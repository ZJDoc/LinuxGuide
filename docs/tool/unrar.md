
# [unrar]解压缩rar文件

今天需要解压`HMDB51_org.tar`文件，它是一个双重压缩文件，找了很多资料，记录一下

*Note：参考中使用了rar，服务器上只安装了unrar，效果是一样的*

## 使用

先解压第一层

```
$ unrar x hmdb51_org.rar hmdb51_org/
```

将解压文件保存在`hmdb51_org`目录下，解压得到了`51`个`.rar`文件

```
$ ls hmdb51_org
brush_hair.rar    fencing.rar    punch.rar        somersault.rar
cartwheel.rar     flic_flac.rar  push.rar         stand.rar
catch.rar         golf.rar       pushup.rar       swing_baseball.rar
chew.rar          handstand.rar  ride_bike.rar    sword_exercise.rar
clap.rar          hit.rar        ride_horse.rar   sword.rar
climb.rar         hug.rar        run.rar          talk.rar
climb_stairs.rar  jump.rar       shake_hands.rar  throw.rar
dive.rar          kick_ball.rar  shoot_ball.rar   turn.rar
draw_sword.rar    kick.rar       shoot_bow.rar    walk
dribble.rar       kiss.rar       shoot_gun.rar    walk.rar
drink.rar         laugh.rar      sit.rar          wave.rar
eat               pick.rar       situp.rar
eat.rar           pour.rar       smile.rar
fall_floor.rar    pullup.rar     smoke.rar
```

再将剩下的文件解压

```
$ cd hmdb51_org/
$ ls *.rar | xargs -n1 urar x
```

## 相关阅读

* [UCF101和HMDB51数据集的处理 for Human Action Recognition](https://blog.csdn.net/Amazingren/article/details/105408049)