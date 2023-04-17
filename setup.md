# 使用 Minikube
```shell
minikube start --image-mirror-country='cn' --image-repository='registry.cn-hangzhou.aliyuncs.com/google_containers' --kubernetes-version=v1.23.8
```

# 使用 kubeadm
+ 安装可以按照这个步骤：https://raw.githubusercontent.com/Okabe-Rintarou-0/Cloud-OS-labs/main/k8s%20practice/k8s%E5%AE%9E%E8%B7%B5%E6%8A%A5%E5%91%8A.pdf

## 遇到的问题

+ kubeadm init 初始化报错：container runtime is not running
  https://blog.csdn.net/weixin_46601322/article/details/126722122

+ swapoff  -a
    ```
    #（1）临时关闭swap分区, 重启失效;
    swapoff  -a
 
    #（2）永久关闭swap分区
    swapoff -a && sed -i '/ swap / s/^\(.*\)$/#\1/g' /etc/fstab
    setenforce 0 && sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config
    ``` 

    > kubernetes的想法是将实例紧密包装到尽可能接近100％。 所有的部署应该与CPU /内存限制固定在一起。 所以如果调度程序发送一个pod到一台机器，它不应该使用交换。 设计者不想交换，因为它会减慢速度。