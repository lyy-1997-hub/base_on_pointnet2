# base_on_pointnet2
使用自己的数据集，新增类别。
更改了data文件里的filelist、modelnet40_test、modelnet40_train、shape_names的内容，原有的数据集只剩下airplane和bathtub，然后新增了missile；
以及train.py里的num_class = 3；
还有models文件里的pointnet2_cls_ssg.py最后一层网络输出net = tf_util.fully_connected(net, 40, activation_fn=None, scope='fc3')里的40改了3。
但是运行python train.py --model pointnet2_cls_ssg --batch_size 2 --normal，报错如下：
2020-09-23 14:43:16.029877: W tensorflow/core/common_runtime/bfc_allocator.cc:211] Allocator (GPU_0_bfc) ran out of memory trying to allocate 2.11GiB. 
The caller indicates that this is not a failure, but may mean that there could be performance gains if more memory were available.
Traceback (most recent call last):
  File "train.py", line 292, in <module>
    train()
  File "train.py", line 180, in train
    train_one_epoch(sess, ops, train_writer)
  File "train.py", line 206, in train_one_epoch
    batch_data, batch_label = TRAIN_DATASET.next_batch(augment=True)
  File "/media/yy/Data/ipython_jupyter/pointnet2123/modelnet_dataset.py", line 123, in next_batch
    ps,cls = self._get_item(self.idxs[i+start_idx])
  File "/media/yy/Data/ipython_jupyter/pointnet2123/modelnet_dataset.py", line 80, in _get_item
    cls = self.classes[self.datapath[index][0]]
KeyError: ''
