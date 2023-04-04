<!DOCTYPE html>
<html>

<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width">
    <script src="jquery.min.js"></script>
    <script src="jquery-ui/jquery-ui.js"></script>
    <script src="jquery-ui/jquery-ui.css"></script>
    <script src="https://code.jquery.com/jquery-3.6.0.js"></script>
    <script src="https://code.jquery.com/ui/1.13.2/jquery-ui.js"></script>
    <link rel="stylesheet" href="//code.jquery.com/ui/1.13.2/themes/base/jquery-ui.css">
    <title>
        Code Runner
    </title>
    <style>
        #buttons {
            width: 250px;
            margin: 0 auto;
        }

        button {
            margin-bottom: 10px;
            margin-top: 10px;
        }

        button:hover {
            background-color: #fff;
            border: rgb(83, 83, 83) 1px solid;
        }

        textarea {
            float: left;
            font-family: 'Courier New', Courier, monospace;
        }

        iframe {
            float: left;
        }

        textarea {
            resize: none;
            font-size: 100%;
        }

        .active {
            background-color: #77eaa9;
        }

        .hide {
            display: none;
        }

        #out {
            position: relative;
            top: -20px;
        }

        h1 {
            margin: 0 auto;
            width: 240px;
            color: #0c0d12;
            font-family: 'Courier New', Courier, monospace;
        }

        body {
            margin: 0;
            padding: 0;
        }

        #container {
            background-color: #bcf5f7;
        }

        iframe {
            border: none;
        }

        textarea {
            border: #bcf5f7 solid 5px;
            border-top: none;
            border-bottom: none;
        }

        button {
            padding: 1dvb;
            border-radius: 50px;
            border: gray 1px solid;
            background-color:#ededed;
            font-family: 'Courier New', Courier, monospace;
        }
        textarea
        {
            outline:none;
            overflow:auto;
        }
        textarea:focus
        {
            background-color: rgb(241, 241, 241);
        }

        #csspanel {
            border-left: none;
        }
        #htmlpanel {
            border-left: none;
        }

        #jspanel {
            border-left: none;
        }
    </style>
</head>

<body>
    <div id="container">
        <h1>Code Runner</h1>
        <div id="buttons">
            <button id="html" class="panel">HTML</button>
            <button id="css" class="panel">CSS</button>
            <button id="js" class="panel">Javascript</button>
            <button id="output" class="panel">Output</button>
        </div>
        <div id="main">
            <textarea id="htmlpanel" placeholder="html" class="hide" spellcheck="false"><h2>Output</h2></textarea>
            <textarea id="csspanel" class="hide" placeholder="css" spellcheck="false"></textarea>
            <textarea id="jspanel" class="hide" spellcheck="false" placeholder="javascript"></textarea>
            <iframe id="outputpanel" class="hide"></iframe>
        </div>
    </div>
    <script type="text/javascript">

        function initial() {
            $("#htmlpanel").show();
            $("#outputpanel").show();
            $("#html").addClass("active");
            $("#output").addClass("active");
            $("#html").css("border", "gray 1px solid");
            $("#output").css("border", "gray 1px solid");
        }
        initial();
        updateIframe();
        resize();
        function updateIframe() {
            $("iframe").contents().find("html").html($("#htmlpanel").val());
            $("iframe").contents().find("head").html("<style>" + $("#csspanel").val() + "</style>");
            document.getElementById("outputpanel").contentWindow.eval($("#jspanel").val());
        }

        $(function () {
            $("textarea").on("change keyup paste", function () {
                updateIframe();
            });
        });
        function resize() {
            var numItems = $('.hide').filter(function () {
                return $(this).css('display') !== 'none';
            }).length;
            $("textarea").width($(window).width() / numItems - 9);
            $("iframe").width($(window).width() / numItems -9);
        }

        $("textarea").height($(window).height() - $("#container").height() - 4);
        $("iframe").height($(window).height() - $("#container").height() - 4);

        $("button").click(function () {
            $("#" + this.id + "panel").toggle();
            resize();
        })
        $("button").click(function () {
            $(this).toggleClass("active");
            $(this).css("border", "gray 1px solid");
        })
    </script>
</body>

</html>
