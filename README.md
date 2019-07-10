# video
从app或ios传参获取url赋值打开h5手机端直接视频播放




1.今天爬了很多坑，一直想给video和source 的src动态赋值；其实赋值是赋值上了，但是默认打开浏览器后，就不会再调起video了 ，所以他识别不到新赋值的值，替大家爬了一个小时的坑，给大家瞅瞅；

 

步骤一 获取安卓手机或ios手机从http传过来的参数；

        function urlPara2(name) {
            var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
            var r = window.location.search.substr(1).match(reg);
            if (r != null) return r[2];
            return null;
        };
        console.log(urlPara2("url"))；
注意：url需为是安卓或者ios通过http带过来的参数；

 
步骤二  动态追加一个video（文件已经写了video动态赋值后不会播放，所以需要动态append）

    var sourceDom = $("<video src=\""+ urlPara2("url") +"\" loop='loop' autoplay='autoplay' id='player1' type='video/mp4' controls='controls' preload='none'> </video>");
    $('#video1').append(sourceDom);

 

全部代码显示；

 

<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title></title>
    <meta name="Keywords" content="">
    <meta name="Description" content="">

    <!-- 移动设备支持 -->
    <meta content="text/html; charset=UTF-8" http-equiv="Content-Type">
    <meta content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, user-scalable=no" name="viewport">
    <meta content="no-cache,must-revalidate" http-equiv="Cache-Control">
    <meta content="no-cache" http-equiv="pragma">
    <meta content="0" http-equiv="expires">
    <meta http-equiv="X-UA-Compatible" content="IE=Edge,chrome=1">
    <meta content="telephone=no, address=no" name="format-detection">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">

    <link rel="stylesheet" type="text/css" href="css/reset.css">
    <link rel="stylesheet" type="text/css" href="css/pxtorem.css">
    <link rel="stylesheet" type="text/css" media="screen" href="css/style.css">
    <link rel="stylesheet" href="css/mediaelementplayer.css" />
    <style>
        html,body{
            height: 100%;
        }
        #wrap {
            height: 100%;
        }
        .mejs-container,.video,.mejs-poster,.mejs-overlay,.mejs-mediaelement,video {height: 100% !important;width:16rem !important;}
    </style>
</head>

<body>
    <div id="wrap" class="bgColor">
        <div class="clr over video" id="video1">

        </div> 
<!--   <div class="clr over video" id="video2">
      <video src="https://outin-12f4575a97d211e9b81300163e1c8a9c.oss-cn-shanghai.aliyuncs.com/3112c0708891467cbc95eb148ec55f11/12dfa2ef31f5453fbe0bbe47ee76a3b0-4243d5c4f601b2e22d0b433739cc9e21-fd.mp4" type="video/mp4" id="player1"  poster="images/cblx.jpg"  autoplay="autoplay" loop="loop"
      controls="controls" preload="none"></video>
  </div>  -->
</div>

<script src="js/jquery.min.js"></script>
<script src="js/fastclick.js"></script>
<script src="js/pxtorem.js"></script>
<script src="js/mediaelement-and-player.min.js"></script>
<script type="text/javascript">
    $('audio,video').mediaelementplayer({
        success: function(player, node) {
            $('#' + node.id + '-mode').html('mode: ' + player.pluginType);
        }
    });
    $('#stopall').click(function() {
        $('video, audio').each(function() {
            $(this)[0].player.pause();          
        });
    });
    $(function () {
        function urlPara2(name) {
            var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)", "i");
            var r = window.location.search.substr(1).match(reg);
            if (r != null) return r[2];
            return null;
        };
        
        var sourceDom = $("<video src=\""+ urlPara2("url") +"\" loop='loop' autoplay='autoplay' id='player1' type='video/mp4' controls='controls' preload='none'> </video>");
        $('#video1').append(sourceDom)


        
        if  (screen.height == 812) {
        $("#video1").remove();//此分辨率下你需要的操作
    } else {
        $("#video2").remove();//默认操作
    }
});    
</script>
</body>
</html>

 

 

需要其他详细代码联系我

微博：艾米的猫儿

趁时光不老，努力活成自己想要的样子 笑看过往

QQ/微信:731335498
--------------------- 
作者：qq_731335498 
来源：CSDN 
原文：https://blog.csdn.net/qq_731335498/article/details/95342679 
版权声明：本文为博主原创文章，转载请附上博文链接！
