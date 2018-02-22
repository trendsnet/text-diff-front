<template>
    <my-page title="文本比较、合并">
        <div>
            <div id="mergely-resizer">
                <div id="diff">
                </div>
            </div>
        </div>
        <ui-row gutter>
            <ui-col width="50" tablet="50" desktop="50">
                <ui-raised-button class="file-btn" label="从文件中导入">
                    <input type="file" class="ui-file-button" @change="fileChange($event, 1)">
                </ui-raised-button>
                <label>编码：</label>
                <select id="l_encode" value="UTF-8" class="span1" onchange="setLeftCode();">
                    <option value="UTF-8">UTF-8</option>
                    <option value="GBK">GBK</option>
                    <option value="GB2312">GB2312</option>
                    <option value="GB18030">GB18030</option>
                    <option value="ISO-8859-2">ISO-8859-2</option>
                </select>
                <div class="download-box">
                    <ui-raised-button label="下载" @click="downloadLeft" />
                </div>
            </ui-col>
            <ui-col width="50" tablet="50" desktop="50">
                <ui-raised-button class="file-btn" label="从文件中导入">
                    <input type="file" class="ui-file-button" @change="fileChange($event, 2)">
                </ui-raised-button>
                <label>编码：</label>
                <select id="r_encode" value="UTF-8" class="span1" onchange="setRightCode();">
                    <option value="UTF-8">UTF-8</option>
                    <option value="GBK">GBK</option>
                    <option value="GB2312">GB2312</option>
                    <option value="GB18030">GB18030</option>
                    <option value="ISO-8859-2">ISO-8859-2</option>
                </select>
                <div class="download-box">
                    <ui-raised-button label="下载" @click="downloadRight" />
                </div>
            </ui-col>
        </ui-row>
    </my-page>
</template>

<script>
    /* eslint-disable */
    export default {
        data () {
            return {
            }
        },
        mounted() {
            var l_files;
            var r_files;

            $('#diff').mergely({
                cmsettings: { readOnly: false },
                lhs: function(setValue) {
                    setValue('这是第一段文本\n这是第2段文本\n这是第三段文本\n这是第四段文本');
                },
                rhs: function(setValue) {
                    setValue('这是第一段文本\n这是第二段文本\n这是第三段文本\n这是第4段文本');
                }
            });
            
            

            

            function leftFileSelect(files) {
                l_files=files;
                setLeft(l_files);
            }

            function rightFileSelect(files){
                r_files=files;
                setRight(r_files);
            }

            function setRight(files){
                f=files[0];
                var reader = new FileReader();
                reader.onload = (function(file) {
                    return function(e) {
                        $('#diff').mergely("rhs",this.result);
                    };
                })(f);
                reader.readAsText(f,$('#r_encode').val());
            }

            function setLeft(files){
                let f=files[0];
                var f_name=f.name;
                var f_type=f_name.substring(f_name.lastIndexOf("."));
                switch(f_type){
                    case ".js":
                        setRender("javascript/javascript.js");
                        break;
                    case ".css":
                        setRender("css/css.js");
                        break;
                    case ".go":
                        setRender("go/go.js");
                        break;
                    case ".groovy":
                        setRender("groovy/groovy.js");
                        break;
                    case ".c",".cpp":
                        setRender("clike/clike.js");
                        break;
                    case ".php":
                        setRender("php/php.js");
                        break;
                    case ".xml":
                        setRender("xml/xml.js");
                        break;
                    case ".html":
                        setRender("htmlembedded/htmlembedded.js");
                        break;
                    case ".less":
                        setRender("less/less.js");
                        break;
                    case ".lua":
                        setRender("lua/lua.js");
                        break;
                    case ".md":
                        setRender("markdown/markdown.js");
                        break;
                    case ".vm":
                        setRender("velocity/velocity.js");
                        break;
                    case ".py":
                        setRender("python/python.js");
                        break;
                    case ".properties":
                        setRender("properties/properties.js");
                        break;
                    case ".rb":
                        setRender("ruby/ruby.js");
                        break;
                    case ".sh":
                        setRender("shell/shell.js");
                        break;
                    case ".sql":
                        setRender("plsql/plsql.js");
                        break;
                    case ".erl":
                        setRender("erlang/erlang.js");
                        break;
                    case ".coffee":
                        setRender("coffeescript/coffeescript.js");
                        break;
                    case ".pl":
                        setRender("perl/perl.js");
                        break;
                        defualt:setRender("clike/clike.js");
                }
                var reader = new FileReader();
                reader.onload = (function(file) {
                    return function(e) {
                        $('#diff').mergely("lhs",this.result);
                    };
                })(f);
                reader.readAsText(f,$('#l_encode').val());
            }
            function setLeftCode(){
                if(null!=l_files)
                    setLeft(l_files);
            }
            function setRightCode(){
                if(null!=r_files)
                    setRight(r_files);
            }
            function setRender(type){
                var base_src="/js/CodeMirror-2.25/mode/";
                $("#render_js").attr("src",base_src+type);
            }
        },
        methods: {
            fileChange(e, left) {
                function setRender(type){
                    var base_src="/js/CodeMirror-2.25/mode/";
                    $("#render_js").attr("src",base_src+type);
                }
                let _this = this
                let file = e.target.files[0]
                if (left === 1) {
                    var f_name = file.name;
                    var f_type = f_name.substring(f_name.lastIndexOf("."))
                    switch(f_type){
                        case ".js":
                            setRender("javascript/javascript.js");
                            break;
                        case ".css":
                            setRender("css/css.js");
                            break;
                        case ".go":
                            setRender("go/go.js");
                            break;
                        case ".groovy":
                            setRender("groovy/groovy.js");
                            break;
                        case ".c",".cpp":
                            setRender("clike/clike.js");
                            break;
                        case ".php":
                            setRender("php/php.js");
                            break;
                        case ".xml":
                            setRender("xml/xml.js");
                            break;
                        case ".html":
                            setRender("htmlembedded/htmlembedded.js");
                            break;
                        case ".less":
                            setRender("less/less.js");
                            break;
                        case ".lua":
                            setRender("lua/lua.js");
                            break;
                        case ".md":
                            setRender("markdown/markdown.js");
                            break;
                        case ".vm":
                            setRender("velocity/velocity.js");
                            break;
                        case ".py":
                            setRender("python/python.js");
                            break;
                        case ".properties":
                            setRender("properties/properties.js");
                            break;
                        case ".rb":
                            setRender("ruby/ruby.js");
                            break;
                        case ".sh":
                            setRender("shell/shell.js");
                            break;
                        case ".sql":
                            setRender("plsql/plsql.js");
                            break;
                        case ".erl":
                            setRender("erlang/erlang.js");
                            break;
                        case ".coffee":
                            setRender("coffeescript/coffeescript.js");
                            break;
                        case ".pl":
                            setRender("perl/perl.js");
                            break;
                            defualt:setRender("clike/clike.js");
                    }
                }
                
                _this.result = {}

                let reader = new FileReader()
                reader.onload = e => {
                    let content = e.target.result
                    if (left === 1) {
                        $('#diff').mergely("lhs", content);
                    } else {
                        $('#diff').mergely("rhs", content);
                    }
                }
                let encode = left === 1 ? $('#l_encode').val() : $('#r_encode').val()
                reader.readAsText(file, encode)
            },
            downloadLeft() {
                var content = $('#diff').mergely('get', 'lhs')
                var blob = new Blob([content], {type: "text/plain;charset=utf-8"})
                saveAs(blob, 'yunser.com-' + new Date().getTime() + '.txt')
            },
            downloadRight() {
                var content = $('#diff').mergely('get', 'rhs')
                var blob = new Blob([content], {type: "text/plain;charset=utf-8"})
                saveAs(blob, 'yunser.com-' + new Date().getTime() + '.txt')
            }
        }
    }
</script>

<style scoped>
</style>

<style>
    .container {
        width: 100%;
        max-width: 100%;
    }
    #mergely-resizer {
        display: block;
        width: 2000px !important;
        margin-bottom: 16px;
        overflow: hidden;
    }
    .form {
        display: block;
        height: 200px;
        margin-bottom: 16px;
        overflow: hidden;
    }
    .ui-file-button{
        position: absolute;
        left: 0;
        right: 0;
        top: 0;
        bottom: 0;
        opacity: 0;
    }
    .download-box {
        margin-top: 16px;
    }
</style>