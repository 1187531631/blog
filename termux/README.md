# termux�����װ-��������
termux��װ����װ���ָ��

### ��Ҫ����

```
apt update
apt upgrade
```

### �������װ����������

```
apt install python python-dev clang fftw libzmq libzmq-dev freetype freetype-dev libpng libpng-dev pkg-config zlib zlib-dev libiconv libiconv-dev curl
```

### ��������ֿ�

```
$ curl -L https://its-pointless.github.io/setup-pointless-repo.sh | sh
```


### ��ѧ����������

```
pip install numpy pandas matplotlib
```

### ��������ѧϰ
```
pkg install scipy 
pip install scikit-learn
```

### ��װdlib ����ʶ��

```
LDFLAGS=" -llog -lpython3" python3 setup.py install --set 'DCMAKE_INSTALL_PREFIX=$PREFIX'
```


### debug����

```
pkg-config --cflags freetype2
```

## TODO
- tensorflow
- keras



