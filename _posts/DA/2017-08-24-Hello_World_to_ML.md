# keras 手写是最识别

```
'''Trains a simple convnet on the MNIST dataset.

Gets to 99.25% test accuracy after 12 epochs
(there is still a lot of margin for parameter tuning).
16 seconds per epoch on a GRID K520 GPU.
'''

from __future__ import print_function
import keras
from keras.datasets import mnist
from keras.models import Sequential
from keras.layers import Dense, Dropout, Flatten
from keras.layers import Conv2D, MaxPooling2D
from keras import backend as K

# batch_size　太小会导致训练慢，过拟合等问题；太大会导致欠拟合．
batch_size = 128
# 这是一个分类问题，识别数字０－９.
num_classes = 10
# 迭代次数
epochs = 12

# input image dimensions
# 输入的图片的像素为28*28
img_rows, img_cols = 28, 28

# the data, shuffled and split between train and test sets
# 导入训练数据集和测试数据集（第一次需要下载）
(x_train, y_train), (x_test, y_test) = mnist.load_data()

# 图片可视化
import matplotlib.pyplot as plt

# %matplotlib inline  # jupyter notebook中使用
# subplot(331):整个做图区域划分为3*3块，第三个参数１表示本次图画在第一个区块中．(顺序为由左到右，又上到下)
for i in range(0, 4):
    plt.subplot(220 + (i + 1))
    plt.imshow(x_train[i], cmap=plt.get_cmap('gray_r'))  # 灰度图片："gray":黑地白字，　"gray_r":白底黑字．
    plt.title(y_train[i])
plt.show()  # IDE中需要使用plt.show()来显示图片

# tensorflow的图片格式为（图片个数，图片宽度，图片高度，通道数）
# theano的图片格式为（图片个数，通道数，图片宽度，图片高度）
# 灰度图片的通道数为１，
if K.image_data_format() == 'channels_first':
    x_train = x_train.reshape(x_train.shape[0], 1, img_rows, img_cols)
    x_test = x_test.reshape(x_test.shape[0], 1, img_rows, img_cols)
    input_shape = (1, img_rows, img_cols)
else:
    x_train = x_train.reshape(x_train.shape[0], img_rows, img_cols, 1)
    x_test = x_test.reshape(x_test.shape[0], img_rows, img_cols, 1)
    input_shape = (img_rows, img_cols, 1)

# 数据类型转为float32，结果更精确．
x_train = x_train.astype('float32')
x_test = x_test.astype('float32')
# 归一化　每一个通道的数据值为0-255，0表示白色，255表示黑色
x_train /= 255
x_test /= 255
print('x_train shape:', x_train.shape)
print(x_train.shape[0], 'train samples')
print(x_test.shape[0], 'test samples')

# convert class vectors to binary class matrices
# 标签转换为独热码，如(0010000000)表示数字2
y_train = keras.utils.to_categorical(y_train, num_classes)
y_test = keras.utils.to_categorical(y_test, num_classes)

# 构建模型
model = Sequential()  # 序列模型
# 第一层为二维卷积层，卷积层改变图片像素
# 32为filters卷积核的个数，也是输出的维度
# kernel_size为卷积核的大小:3*3
# 激活函数选用的是"relu"
# 第一层必须包含输入数据的格式input_shape参数，后面层的input_shape由模型自己计算出来．
model.add(Conv2D(32, kernel_size=(3, 3),
                 activation='relu',
                 input_shape=input_shape))
# 第二层：卷积层
model.add(Conv2D(64, (3, 3), activation='relu'))
# 第三层：最大池化层
model.add(MaxPooling2D(pool_size=(2, 2)))
# 第四层：Dropout层，对于池化层的输出，暂时丢弃25%的神经元
model.add(Dropout(0.25))
# 第五层：Flatten层，数据一维化
model.add(Flatten())
# 第六层：全连接层，
# 输出128维数据，激活函数选用"softmax"
model.add(Dense(128, activation='relu'))
# 第七层：Dropout层
model.add(Dropout(0.5))
# 第八层：全连接层
# 输出10类数据，激活函数为"softmax"
model.add(Dense(num_classes, activation='softmax'))

# 编译模型，配置模型的学习过程
# 损失函数选用交叉熵，优化器选用Adadelta，将识别准确率作为模型评估指标
model.compile(loss=keras.losses.categorical_crossentropy,
              optimizer=keras.optimizers.Adadelta(),
              metrics=['accuracy'])

# 训练模型:fit
# 由训练数据集x_train,y_train拟合模型曲线，再用验证数据集来验证模型的好坏

# batch_size:整数，指定进行梯度下降时每个batch包含的样本数．
# 训练时一个batch的样本会被就算一次梯度下降，使目标函数优化一次．

# epochs:整数，训练的轮数．每个epoch会把训练集轮一遍．

# verbose:日志显示，0为不在标准输出流中输出日志信息，１为输出进度条进度，
# ２为每个epoch输出一行记录

# validation_data:形式为（X, y）的tuple，是指定的验证集．此参数将覆盖validation_split

# validation_split:０－１之间的浮点数，用来指定训练集的一定比例的数据作为验证集．
# 验证集不参与训练，但是会在每个epoch结束后测试模型的指标，如损失函数，精度等．
# 注意validation_split的划分是在shuffle(洗，改组)之前的，因此如果数据本身是有序的，
# 需要先手工打乱再指定validation_split，否则可能会出现验证集样本不均匀．

# shuffle:布尔值或字符串，一般为布尔值，表示是否在训练过程中随即打乱输入样本的顺序．
# 若为字符串＂batch＂，则是用来处理HDF5数据的特殊情况，它将在batch内部将数据打乱．

# class_weight:字典，将不同的类别映射为不同的权值，
# 该参数用来在训练过程中调整损失函数（只能用于训练）．

# sample_weight：权值的numpy array，用于在训练时调整损失函数（仅用于训练）．
# 可以传递一个1D的与样本等长的向量用于对样本进行1对1的加权，或者在面对时序数据时，
# 传递一个的形式为（samples，sequence_length）的矩阵来为每个时间步上的样本赋不同的权．
# 这种情况下请确定在编译模型时添加了sample_weight_mode='temporal'．

# initial_epoch:从该参数指定的epoch开始训练，在继续之前的训练时有效．

# fit函数返回一个History的对象，其History.history属性记录了损失函数和其他指标的数值随epoch
# 变化的情况，如果有验证集的话，也包含了验证集的这些指标的变化情况．
hist = model.fit(x_train, y_train,
                 batch_size=batch_size,
                 epochs=epochs,
                 verbose=1,
                 shuffle=True,
                 validation_data=(x_test, y_test))
with open("output_fit.txt", "w") as f:
    f.write(str(hist.history))

# 评估模型

# evaluate()按batch计算在某些输入数据上模型的误差，其参数有：
# x:输入数据，与fit一样，是numpy array或numpy array list
# y:标签，numpy array

# batch_size:整数，指定进行梯度下降时每个batch包含的样本数．
# 训练时一个batch的样本会被就算一次梯度下降，使目标函数优化一次．

# verbose:日志显示，0为不在标准输出流中输出日志信息，１为输出进度条进度，只能取０或１

# sample_weight: numpy array，含义同fit的同名参数

# 本函数返回一个测试误差的标量值（如果模型没有其他评价指标），
# 或一个标量的list（如果模型还有其他的评价指标）．
# model.metrics_names将给出list中各个值的含义．
score = model.evaluate(x_test, y_test, verbose=0)
print("metrics_name: ", model.metrics_names)

print('Test loss:', score[0])
print('Test accuracy:', score[1])

```
