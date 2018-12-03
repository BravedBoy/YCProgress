# YCProgress
进度条
## 目录介绍
- 1.本库优势亮点
- 2.使用介绍
    - 2.1 圆环百分比进度条
    - 2.2 直线百分比进度条
    - 2.3 仿杀毒类型百分比进度条
- 3.注意要点
- 4.效果展示
- 5.其他介绍



### 1.本库优势亮点
- 圆环百分比进度条
    - 简便且小巧，支持设置多种属性
- 仿杀毒类型百分比进度条
    - 支持设置多种类型，比如设置百分比+单位类型，或者设置空类型【也就是不显示中间百分比】
    - 支持设置进度条的颜色，未更新的进度条颜色；设置百分比文字大小，颜色；支持设置单位等多种属性
    - 支持允许多线程访问，对于设置setProgress，添加synchronized关键字修饰。设置进度progress，如果小于0或者大于100，则抛异常。避免开发者使用造成其他问题。
- 针对进度条，对于设置color颜色的方法，增加了注解@ColorInt，限制开发者调用color资源
- 使用注解代替了枚举，针对设置枚举的方法，使用注解限制开发者调用时传入的类型。具体可以代码案例！
- 注释十分详细，作为开源的lib库，我觉得要让使用者一目了然。方便调用同时，知道每个方法的作用。



### 2.使用介绍
- 集成库：compile 'cn.yc:YCProgressLib:1.2.6'

#### 2.1 圆环百分比进度条
- 在布局中
    ```
    //也可以设置布局中的attr属性
    <com.ns.yc.ycprogresslib.CircleProgressbar
        android:id="@+id/pb_1"
        android:layout_width="100dp"
        android:layout_height="100dp"
        android:text="进度条" />
    
    ```
- 使用方法
    ```
    //设置类型
    pb_1.setProgressType(ProgressBarUtils.ProgressType.COUNT);
    //设置圆形的填充颜色
    pb_1.setInCircleColor(getResources().getColor(R.color.redTab));
    //设置外部轮廓的颜色
    pb_1.setOutLineColor(getResources().getColor(R.color.grayLine));
    //设置进度监听
    pb_1.setCountdownProgressListener(1, progressListener);
    //设置外部轮廓的颜色
    pb_1.setOutLineWidth(2);
    //设置进度条线的宽度
    pb_1.setProgressLineWidth(5);
    //设置进度
    pb_1.setProgress(60);
    //设置倒计时总时间
    pb_1.setTimeMillis(3000);
    //设置进度条颜色
    pb_1.setProgressColor(getResources().getColor(R.color.colorPrimary));
    
    //开始
    pb_1.start();
    //暂停
    pb_1.stop();
    //重新开始
    pb_1.reStart();
    ```



#### 2.2 直线百分比进度条
- 在布局中
    ```
    <com.ns.yc.ycprogresslib.NumberProgressbar
        android:id="@+id/bar1"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
    
    <com.ns.yc.ycprogresslib.NumberProgressbar
        android:id="@+id/bar2"
        android:layout_marginTop="10dp"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:progress_max="100"
        app:progress_reached_bar_height="3dp"
        app:progress_unreached_bar_height="3dp"
        app:progress_reached_color="@color/colorPrimary"
        app:progress_unreached_color="@color/gray3"
        app:progress_text_size="14sp"
        app:progress_text_color="@color/colorAccent"
        app:progress_text_visibility="visible"/>
    ```
- 代码调用
    ```
    bar1 = (NumberProgressbar) findViewById(R.id.bar1);
    //设置倒计时总时间
    bar1.setTimeMillis(10000);
    //设置最大进度条的值
    bar1.setMax(100);
    //设置进度条文本的颜色
    bar1.setProgressTextColor(this.getResources().getColor(R.color.colorAccent));
    //设置进度条文本的大小
    bar1.setProgressTextSize(ProgressBarUtils.sp2px(this,14));
    //设置百分比文字内容是否可见
    bar1.setNumberTextVisibility(ProgressBarUtils.NumberTextVisibility.Visible);
    //设置百分比进度条的高度
    bar1.setReachedBarHeight(10);
    //设置未更新百分比进度条的高度
    bar1.setUnreachedBarHeight(10);
    //设置百分比进度条的颜色
    bar1.setReachedBarColor(this.getResources().getColor(R.color.redTab));
    //设置未更新百分比进度条的颜色
    bar1.setUnreachedBarColor(this.getResources().getColor(R.color.blackText2));
    //设置百分比进度条的监听
    bar1.setOnProgressBarListener(new OnNumberProgressListener() {
        @Override
        public void onProgressChange(int current, int max) {
    
        }
    });
    
    //开始
    bar1.start();
    //暂停
    bar1.stop();
    ```


#### 2.3 仿杀毒类型百分比进度条
- 布局代码
    ```
    <com.ns.yc.ycprogresslib.RingProgressBar
        android:id="@+id/bar_percent"
        android:layout_width="100dp"
        android:layout_height="100dp"/>
    ```
- 如何调用
    ```
    bar_percent = (RingProgressBar) findViewById(R.id.bar_percent);
    //设置进度
    bar_percent.setProgress(0);
    //设置更新进度条颜色
    bar_percent.setDotColor(this.getResources().getColor(R.color.colorAccent));
    //设置未更新部分的进度条颜色
    bar_percent.setDotBgColor(this.getResources().getColor(R.color.blackText));
    //设置百分比文字颜色
    bar_percent.setPercentTextColor(this.getResources().getColor(R.color.blackText1));
    //设置百分比文字大小
    bar_percent.setPercentTextSize(ProgressBarUtils.dp2px(this,16.0f));
    //设置展示的类型
    bar_percent.setShowMode(ProgressBarUtils.RingShowMode.SHOW_MODE_PERCENT);
    //设置单位的文字内容
    bar_percent.setUnitText("%");
    //设置单位的文字大小
    bar_percent.setUnitTextSize(ProgressBarUtils.dp2px(this,16.0f));
    //设置单位的文字颜色
    bar_percent.setUnitTextColor(this.getResources().getColor(R.color.blackText1));
    ```
- 可以设置多种类型
    - 第一种：百分比+单位【支持自己设置单位，比如设置%，或者设置毫秒s等】
    - 第二种：空显示模式【也就是不显示中间的部分】



### 3.注意要点
- 3.1 不论是圆环进度条还是直线进度条，在调用setProgress设置进度时，增加了验证进度的功能。因为如果设置值超过100或者小于0，该方法就起作用呢！
    ```
    /**
     * 验证进度。
     *
     * @param progress      你要验证的进度值。
     * @return              返回真正的进度值。
     */
    private int validateProgress(int progress) {
        if (progress > 100){
            progress = 100;
        } else if (progress < 0){
            progress = 0;
        }
        return progress;
    }
    ```
- 3.2 针对CircleProgressbar和NumberProgressbar自定义控件，如果调用start方法开始循环执行setProgress，程序意外销毁，则注意：
    ```
    /**
     * 当自定义控件销毁时，则调用该方法
     */
    @Override
    protected void onDetachedFromWindow() {
        super.onDetachedFromWindow();
        stop();
    }
    ```



### 4.效果展示
- ![image](https://github.com/yangchong211/YCProgress/blob/master/image/1.jpg)
![image](https://github.com/yangchong211/YCProgress/blob/master/image/2.jpg)
![image](https://github.com/yangchong211/YCProgress/blob/master/image/3.jpg)
![image](https://github.com/yangchong211/YCProgress/blob/master/image/4.jpg)
![image](https://github.com/yangchong211/YCProgress/blob/master/image/5.jpg)
![image](https://github.com/yangchong211/YCProgress/blob/master/image/6.jpg)


### 5.其他介绍
#### 关于其他内容介绍
![image](https://upload-images.jianshu.io/upload_images/4432347-7100c8e5a455c3ee.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


#### 版本更新说明
- v1.0.0  更新于2016/2/10          作用于投资界下载更新进度条，学习自定义控件
- v1.1.1  更新于2016/8/12          针对圆环进度条，添加自定义attr属性
- v1.1.2  更新于2017/3/10          针对圆环进度条添加设置倒计时总时间，start和stop方法
- v1.1.3  更新于2017/5/27          针对设置进度的方法，增加校验，不能小于0或者大于100
- v1.2.5  更新于2018年8月24日       添加了直线百分比进度条，针对部分方法添加注解
- v1.2.6  更新于2018年11月30日      添加了详细的注释
- 关于直线百分比进度条参考了代码家NumberProgressBar项目：https://github.com/daimajia/NumberProgressBar



#### 关于博客汇总链接
- 1.[技术博客汇总](https://www.jianshu.com/p/614cb839182c)
- 2.[开源项目汇总](https://blog.csdn.net/m0_37700275/article/details/80863574)
- 3.[生活博客汇总](https://blog.csdn.net/m0_37700275/article/details/79832978)
- 4.[喜马拉雅音频汇总](https://www.jianshu.com/p/f665de16d1eb)
- 5.[其他汇总](https://www.jianshu.com/p/53017c3fc75d)


#### 其他推荐
- 博客笔记大汇总【15年10月到至今】，包括Java基础及深入知识点，Android技术博客，Python学习笔记等等，还包括平时开发中遇到的bug汇总，当然也在工作之余收集了大量的面试题，长期更新维护并且修正，持续完善……开源的文件是markdown格式的！同时也开源了生活博客，从12年起，积累共计47篇[近20万字]，转载请注明出处，谢谢！
- 链接地址：https://github.com/yangchong211/YCBlogs
- 如果觉得好，可以star一下，谢谢！当然也欢迎提出建议，万事起于忽微，量变引起质变！


#### 关于LICENSE
```
Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```











