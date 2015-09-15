#一、文件介绍

   1.piazza_cid_xblock:是根据cid只显示某个特定的讨论记录的xblock
   
   2.piazza_feed_xblock:是根据标签筛选讨论记录的xblock。其中下拉菜单列出所有的标签，其他的是popular的标签。
   
   3.piazza_together_xblock：是提供了三种显示方式的xblock：
   
      （1）只显示指定cid的讨论记录的页面；
      （2）只显示根据标的签筛选讨论记录的页面；
      （3）两者同时显示，与piazza界面基本相同；
      
      
#二、XBlock的安装。(以piazza_together_xblock的安装为例)

   1.把在线代码编辑器xblock克隆到edx服务器

        sudo git clone https://github.com/xyongcn/piazza-data-tsinghua.edu.cn_spring2015_30240243x/tree/master/piazzaXBlock/piazza_together_xblock
   
   2.把staticfiles文件夹克隆到edx服务器  
    
        sudo git clone https://github.com/xyongcn/piazza-data-tsinghua.edu.cn_spring2015_30240243x/tree/master/staticfiles/example-together/
  
   3.安装xblock

         sudo -u edxapp /edx/bin/pip.edxapp install /home/zyni/piazza_together_xblock/
        注意： /home/zyni/piazza_together_xblock/ 替换成你刚刚clone的piazza_together_xblock所在路径
         
   4.把example-together复制到下面的目录

        /edx/var/edxapp/staticfiles/
        运用命令：sudo cp -r /home/zyni/example-together/ /edx/var/edxapp/staticfiles/
        
   5.使xblock可用

     1）edx-platform/lms/envs/common.py中去掉注释：

         # from xmodule.x_module import prefer_xmodules
         # XBLOCK_SELECT_FUNCTION = prefer_xmodules
 
     2）edx-platform/cms/envs/common.py,中去掉注释：

        # from xmodule.x_module import prefer_xmodules
        # XBLOCK_SELECT_FUNCTION = prefer_xmodules、
 
     3）edx-platform/cms/envs/common.py中把

       'ALLOW_ALL_ADVANCED_COMPONENTS': False,
        改成：
       'ALLOW_ALL_ADVANCED_COMPONENTS': True,

  6.在Studio中把在线代码编辑器block添加到课程的高级设置中。

         1）登录到Studio,打开你的课程
         2）settings->Advanced Setting
         3)把键”advanced_modules”的值改为piazza.

  7.把在线代码编辑器block添加到课程，在studio中

       1）Edit编辑一个单元
       2）Advanced->piazza

  8.重启edx服务

         sudo /edx/bin/supervisorctl -c /edx/etc/supervisord.conf restart edxapp:
  
安装好之后就可以在cms中看到并使用该组件
      