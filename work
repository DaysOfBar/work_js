var recordId = 0;
var showChatWindow, showFriends, initWechatBox;
var showChatRecords;
var showFriendInfo;
var getFriendInfo;
var sendMsgToFriend;
var getFriends;
var getChats;
var deleteFriend;
var friends;
var new_msg;
var chatRecords;
var sendMsg;
var getStrangers;
var showStrangerInfo;
var getStrangerInfo;
var acceptStranger;
var replyStranger;
var showAddFriend;
var showEmojiPanel;
var layer;
var $;
var flow;
var voice;
var getChatRecord;
var getWeChats;
var getMedia;
var checkingDownloadStatus;
var requestFriendSnsPage;
var getFriendSnsPages;
var viewOuterContent;
var getSnsMedia;
var checkingSnSDownloadStatus;
var getCustomerInfo;
var showCustomerInfo;
var getMediaV2;
var requestSyncFriends;
var newStranger;
var removeMaterial;
var getFriendTags;
var showFriendTags;
var removeTag;
var editTag;
var editMess;
var displayAvailableTagsBlock;

var showTagWindow;
var getTags;
var getTagFriend;

var getMaterialGroups;
var getMaterials;
var sendMaterial;

var showSendImg;

var setMsgRead;
var buildWeChat;

var showSnsTabContent;
var showMaterialTabContent;

var right_click;
var cancel_right_click;
var getSingerWeChats;
var friendRemark;

showFriends = function (elemId, boardId) {
    var obj = $("#" + elemId);
    obj.find(".wechat_board_right_friends").css("display", "block");
    obj.find(".wechat_board_right_chat").css("display", "none");
    obj.find(".board_swich_chat").css("color", "#c2c2c2");
    obj.find(".board_swich_friend").css("color", "#5FB878");
    obj.find(".wechat_board_right_tags").css("display", "none");
    obj.find(".board_swich_tag").css("color", "#c2c2c2");
    var searchObj = $('#board' + boardId).find('input[name=search_friend]');
    searchObj.val('');
    rebuildFriendList(boardId);
    //时间2022/2/13 14:23
    getStrangers(boardId);//获取陌生人消息
    requestSyncFriends(boardId);
    getFriends(boardId);

    showStrangerDot(false, boardId);


    var height = $('#LAY_wechat_content').height();
    var strangerListHeight = (height - 42 - 48 - 42 - 42 - 14);
    obj.find(".wechat_stranger_list").height(strangerListHeight + "px");
    var friendListHeight = (height - 42 - 48 - 42 - 42 - 14);
    obj.find(".wechat_friend_list").height(friendListHeight + "px");
};

var rebuildFriendList = function (boardId) {
    var listObj = $('#wechat_friend_list_' + boardId);
    var listParentObj = listObj.parent();
    listObj.remove();
    listParentObj.append('<div class="layui-col-sm12 wechat_friend_list" id="wechat_friend_list_' + boardId + '" style="overflow: hidden;overflow-y:auto; ">');
};

var rebuildChatList = function (boardId) {
    var listObj = $('#wechat_chat_list_' + boardId);
    var listParentObj = listObj.parent();
    listObj.remove();
    listParentObj.append('<div class="layui-col-sm12 wechat_chat_list" id="wechat_chat_list_' + boardId + '" style="overflow: hidden;overflow-y:auto; ">');
};

var showDot = function (display, boardId, friendId, unreadMsgCount, weChatUnreadMsgCount) {
    if (unreadMsgCount == undefined) {
        unreadMsgCount = 0;
    }
    if (weChatUnreadMsgCount == undefined) {
        weChatUnreadMsgCount = '';
    }
    var unreadMsgCountBadge = 'layui-badge';//'layui-badge-dot';
    var board, weChatList, weChatNav, tab, swichChat, chatList, chat, weChatDot, tabDot, swichDot, chatDot, weChat;
    board = $('#board' + boardId);
    weChatList = $('#LAY_wechat_list');
    weChatNav = weChatList.find("a[data-id=" + boardId + "]");
    weChatDot = weChatNav.find('.' + unreadMsgCountBadge);
    tab = $('.layui-tab-card').find("li[lay-id=" + boardId + "]");
    if (tab) {
        tabDot = tab.find('.' + unreadMsgCountBadge);
    }
    swichChat = board.find('.board_swich_chat');
    swichDot = swichChat.find('.' + unreadMsgCountBadge);
    if (friendId) {
        chatList = board.find('.wechat_chat_list');
        if (chatList) {
            chat = chatList.find('#friend' + friendId);
            chatDot = chat.find('.' + unreadMsgCountBadge);
        }
    }
    if (display == true) {
        if (weChatDot) {
            weChatDot.remove();
            if (weChatUnreadMsgCount > 0) {
                weChatNav.append('<span class="' + unreadMsgCountBadge + '" style="position: absolute;right:1px;z-index: 999999;">' + weChatUnreadMsgCount + '</span>');
            }
        }
        if (tabDot) {
            tabDot.remove();
            if (weChatUnreadMsgCount > 0) {
                tab.append('<span class="' + unreadMsgCountBadge + '" style="position: absolute;left:1px;z-index: 999999;">' + weChatUnreadMsgCount + '</span>');
            }
        }
        if (swichDot) {
            swichDot.remove();
            if (weChatUnreadMsgCount > 0) {
                swichChat.append('<span class="' + unreadMsgCountBadge + '" style="position: absolute;left:1px;z-index: 999999;">' + weChatUnreadMsgCount + '</span>');
            }
        }
        if (chatDot) {
            chatDot.remove();
            if (chat && unreadMsgCount > 0) {
                chat.append('<span class="' + unreadMsgCountBadge + '" style="position: absolute;right:1px;z-index: 999999;">' + unreadMsgCount + '</span>');
            }
        }
        //voice();
        weChatList = $('#LAY_wechat_list');
        weChat = weChatList.find('#w_' + boardId);
        weChat.prependTo(weChatList);
    } else {
        if (weChatDot) weChatDot.remove();
        if (tabDot) tabDot.remove();
        if (swichDot) swichDot.remove();
        if (chatDot) chatDot.remove();
        if (friendId > 0) {
            setMsgRead(boardId, friendId);
        }
    }
};

var showStrangerDot = function (display, boardId) {
    var board = $('#board' + boardId);
    var swichFriend = board.find('.board_swich_friend');
    var swichDot = swichFriend.find('.layui-badge-dot');
    if (display == true) {
        if (swichDot) {
            swichDot.remove();
            swichFriend.append('<span class="layui-badge-dot" style="position: absolute;z-index: 999999;"></span>');
        }
    } else {
        if (swichDot) swichDot.remove();
    }
};

var showStrangerTabDot = function (display, boardId) {
    var board = $('#board' + boardId);
    var strangerTab = board.find('.stranger_tab');
    var dot = strangerTab.find('.layui-badge-dot');
    if (display == true) {
        if (dot) {
            dot.remove();
            strangerTab.append('<span class="layui-badge-dot"></span>');
        }
    } else {
        if (dot) dot.remove();
    }
};

var showStrangerItemDot = function (display, strangerId) {
    var strangerDot = $('#stranger' + strangerId).find('.layui-badge-dot');
    if (display == true) {

    } else {
        if (strangerDot) strangerDot.remove();
    }
};

var rebuildTagList = function (boardId) {
    var listObj = $('#tag_list_' + boardId);
    var listParentObj = listObj.parent();
    listObj.remove();
    listParentObj.append('<div class="layui-col-sm12 tag_list" id="tag_list_' + boardId + '" style="overflow: hidden;overflow-y:auto; ">');
};

layui.use(['element', 'laytpl', 'form', 'table', 'upload'], function () {
    $ = layui.jquery
        , layer = layui.layer
        , flow = layui.flow
        , element = layui.element
        , form = layui.form
        , util = layui.util
        , device = layui.device()
        , $win = $(window)
        , $body = $('body')
        , laytpl = layui.laytpl
        , upload = layui.upload;

    var table = layui.table;

    element.init();

    $body.on('click', '*[layim-event]', function (e) {
        var othis = $(this), methid = othis.attr('layim-event');
        events[methid] ? events[methid].call(this, othis, e) : '';
    });

    var events = {
        playAudio: function (othis) {
            var audioData = othis.data('audio')
                , audio = audioData || document.createElement('audio')
                , pause = function () {
                audio.pause();
                othis.removeAttr('status');
                othis.find('i').html('&#xe652;');
            };
            if (othis.data('error')) {
                return layer.msg('语音消息播放异常');
            }
            if (!audio.play) {
                return layer.msg('您的浏览器不支持audio，请使用谷歌浏览器');
            }
            if (othis.attr('status')) {
                pause();
            } else {
                audioData || (audio.src = othis.data('src'));
                audio.play();
                othis.attr('status', 'pause');
                othis.data('audio', audio);
                othis.find('i').html('&#xe651;');
                //播放结束
                audio.onended = function () {
                    pause();
                };
                //播放异常
                audio.onerror = function () {
                    layer.msg('语音消息播放异常2');
                    othis.data('error', true);
                    pause();
                };
            }
        }
    };

    //触发事件
    var active = {
        tabAdd: function (title, id,deviceIp='',wxid='') {
            //新增一个Tab项
            element.tabAdd('wechat', {
                title: title
                , content: showWechatBoard(id,deviceIp,wxid)
                , id: id
            });
            initWechatBox(id);
        }
        , tabChange: function (id) {
            //切换到指定Tab项
            element.tabChange('wechat', id);
            $('.layui-tab-item').css('height', '100%');
            autodivheight();
            showDot(false, id, 0);
        }
    };

    voice = function () {
        if (device.ie && device.ie < 9) return;
        var audio = document.createElement("audio");
        audio.src = '/assets/voice/new_msg.mp3';
        audio.autoplay = true;
        audio.load();
    };

    var showWechatBoard = function (boardId,deviceIp,wxid) {
        var board_html = '';
        var fresh = true;
        var getTpl = tpl_wechat_board.innerHTML;
        var data = {"boardId": boardId,"deviceIp":deviceIp,"wxid":wxid};
        laytpl(getTpl).render(data, function (html) {
            board_html = html;
        });
        getWechatInfo(boardId, fresh);
        return board_html;
    };

    showChatWindow = function (elemId, boardId, rebuild, friendId, friendRemark) {
        var obj = $("#" + elemId);
        obj.find(".wechat_board_right_friends").css("display", "none");
        if (friendRemark != '') {
            obj.find("span[name='remark']").html(friendRemark);
        }
        obj.find(".wechat_board_right_chat").css("display", "block");
        obj.find(".board_swich_chat").css("color", "#5FB878");
        obj.find(".board_swich_friend").css("color", "#c2c2c2");
        obj.find(".wechat_board_right_tags").css("display", "none");
        obj.find(".board_swich_tag").css("color", "#c2c2c2");
        var searchObj = $('#board' + boardId).find('input[name=search_chat]');
        searchObj.val('');
        // console.log(showChatWindow)
        getChats(boardId, rebuild, friendId);

        var height = $('#LAY_wechat_content').height();
        var chatListHeight = (height - 60 - 58);
        $(".wechat_chat_list").height(chatListHeight + "px");
    };

    initWechatBox = function (wechatId) {
        getChats(wechatId, 1);
    };

    new_msg = function (msg, newChat) {
        var notify = false;
        if (msg['notify'] && msg['notify'] == true) {
            notify = true;
        }
        if (newChat == true) {
            if ($('#LAY_wechat_list').find('#w_' + msg['wechat_id']).length > 0) {
                console.log('wechat_id.length');
                console.log($('#LAY_wechat_list').find('#w_' + msg['wechat_id']).length)
                addNewChat(msg['wechat_id'], msg['friend_id'], notify);
            } else {
                // console.log('getSingerWeChats')
                // console.log('------------')
                getSingerWeChats(msg['wechat_id'], msg['friend_id'], notify);
            }
        }
        // if (msg['notify'] && msg['notify']==true) {
        //     showDot(true, msg['wechat_id'], msg['friend_id']);
        // }
        var board_html = '';
        var getTpl = tpl_msg.innerHTML;
        var data = {"msg": msg};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        if (board_html && board_html != '') {

            var elm = document.getElementById('record_' + msg['record_id']);
            if (elm) {//消息已展示
                //console.log('消息已展示')
                var record = $('#record_' + msg['record_id']);
                record.find('.layui-icon-loading').css('display', 'none');
                if (msg['status'] == -1 && msg['remark'] != '') {
                    record.find('.msg_remark').html('<i class="layui-icon layui-icon-tips" style="padding:0;color:red;"><label>' + msg['remark'] + '</label></i>');
                }
            } else {//消息未展示
                //console.log('消息未展示')
                var obj = $('#friendChat_' + msg['wechat_id'] + '_' + msg['friend_id']).find('.layim-chat-main');
                var ulObj = obj.find('ul');
                var firstObj = ulObj.find('li').first();
                var lastObj = ulObj.find('li').last();
                var scroll = false;
                if (lastObj.is('li') && firstObj.is('li')) {
                    // console.log(first.html());
                    // console.log(last.html());
                    var firstId = firstObj.attr('id');
                    var lastId = lastObj.attr('id');
                    // console.log('firstId:'+firstId);
                    // console.log('lastId:'+lastId);
                    lastId = Number(lastId.replace('record_', ''));
                    firstId = Number(firstId.replace('record_', ''));
                    if (msg['record_id'] > lastId) {//新消息
                        lastObj.after(board_html);
                        scroll = true;
                        //console.log('New recordId:'+msg['record_id']);
                    } else if (msg['record_id'] < firstId) {//旧消息
                        firstObj.before(board_html);
                        //console.log('Old recordId:'+msg['record_id']);
                    }
                } else {//初始化加载消息
                    ulObj.html(board_html);
                }
                if (scroll == true) {
                    elm = document.getElementById('record_' + msg['record_id']);
                    if (elm) {
                        elm.scrollIntoView();
                    }
                }
            }
        }

    };


    sendMsg = function (wechatId, friendId) {
        var obj = $('#board' + wechatId).find('.new-chat-message');
        if (obj) {
            var textMsg = obj.val().trim();
            if (textMsg == '') {
                layer.msg('消息内容不能为空', {icon: 5});
                return false;
            }
            var post = {
                'id': wechatId,
                'friendId': friendId,
                'textMsg': encodeURIComponent(textMsg)
            };
            layer.msg('发送中...', {
                shadeClose: false
                , icon: 16
                , shade: 0.01
                , time: 500
            });
            $.ajax({
                type: "POST",
                data: post,
                url: "/cs_work/newTextMsgTask",
                success: function (response) {
                    var dataObj = $.parseJSON(response);
                    if (dataObj.code === 0) {
                        // setTimeout(function(){
                        //     freshChartRecords(wechatId, friendId);
                        // }, 1000);
                        if (dataObj.record) {
                            var record = dataObj.record;
                            new_msg(record);
                            var clone = $('#friend'+friendId).clone(true);
                            $('#friend'+friendId).remove();
                            $('#wechat_chat_list_'+wechatId).prepend(clone);
                            //发消息排序
                            var clone = $('#w_'+wechatId).clone(true);
                            $('#w_'+wechatId).remove();
                            $('#LAY_wechat_list').prepend(clone);
                        }
                        if (obj) {
                            obj.val('');
                        }
                    } else {
                        layer.msg(dataObj.msg, {icon: 5});
                    }
                },
                error: function (request, status, error) {
                    layer.msg('哦噢，网络开小差了', {icon: 5});
                }
            });
        }
    };

    newStranger = function (msg) {
        if (msg['notify'] && msg['notify'] == true) {
            showStrangerDot(true, msg['wechat_id']);
        }
    };

    var getWechatInfo = function (wechatId, fresh) {
        return false;
        $.ajax({
            type: "GET",
            url: "/cs_work/get_wechat_info_ajax/" + wechatId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var wechatInfo = dataObj.data;
                    if (fresh == true && wechatInfo.headImage && wechatInfo.headImage != '') {
                        $('#headImage' + wechatId).attr('src', wechatInfo.headImage);
                    }
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    buildWeChat = function (weChatData) {
        // return '<dd id="w_' + (weChatData.id != '' ? weChatData.id : '') + '"><a data-name="' + (weChatData.nickName != '' ? weChatData.nickName : weChatData.wxid) + '" data-id="' + (weChatData.id != '' ? weChatData.id : '') + '" device_url="' + (weChatData.device_url != '' ? weChatData.device_url : '') + '" class="layui-side-wechat" data-type="tabChange"><span class="layui-badge" style="position: absolute;right:1px;z-index: 999999;' + (weChatData.unread_msg_count > 0 ? '' : 'display: none;') + '">' + weChatData.unread_msg_count + '</span>' + (weChatData.status == 1 ? '<span style="float:right;color: green;">在线</span>' : '<span style="float:right;color: red;">离线</span>') + '<img src="'+(weChatData.head != '' ? weChatData.head : '/static/cs/images/default_head.jpeg')+'" width="30px">&nbsp;' + (weChatData.nickName != '' ? weChatData.nickName : weChatData.wxid) + '</a></dd>';
        return '<dd id="w_' + (weChatData.id != '' ? weChatData.id : '') + '" data-top="'+weChatData.is_top+'" oncontextmenu="right_click('+weChatData.id+')" class="'+(weChatData.is_top == 2 ? 'right_click_color':'')+'" >' +
            '<a data-wxid="'+weChatData.wxid+'" device_name="'+weChatData.device_name+'" device_ip="'+weChatData.ip+'" device_mac="'+weChatData.device_mac+'"  data-name="' + (weChatData.nickName != '' ? weChatData.nickName : weChatData.wxid) + '" data-id="' + (weChatData.id != '' ? weChatData.id : '') + '" device_url="' + (weChatData.device_url != '' ? weChatData.device_url : '') + '" class="layui-side-wechat" data-type="tabChange">' +
            '<span class="layui-badge" style="position: absolute;right:1px;z-index: 999999;' + (weChatData.unread_msg_count > 0 ? '' : 'display: none;') + '">' + weChatData.unread_msg_count + '</span>' + (weChatData.status == 1 ? '<span style="float:right;color: green;margin-right: 20px">在线</span>' : '<span style="float:right;color: red;margin-right: 20px;">离线</span>') + '<img src="'+(weChatData.head != '' ? weChatData.head : '/static/cs/images/default_head.jpeg')+'" width="30px">&nbsp;' + (weChatData.nickName != '' ? weChatData.nickName : weChatData.wxid) + '</a>' +
            '</dd>';
    };


    getWeChats = function () {//已改成流加载

        layui.use('flow', function () {
            var flow = layui.flow;
            var element = layui.element;
            element.init();
            flow.load({
                elem: '#LAY_wechat_list' //指定列表容器
                , scrollElem: '#LAY_wechat_list'
                , done: function (page, next) { //到达临界点（默认滚动触发），触发下一页
                    var lis = [];
                    var post = {
                        page: page,
                        limit: 20
                    };
                    // console.log('getWeChats');
                    console.log('-------');
                    console.log('默认滚动触发')

                    $.post('get_wechats_ajax', post, function (dataObj) {
                        //假设你的列表返回在data集合中
                        // var dataObj = $.parseJSON(res);
                        if (dataObj.code === 0) {
                            var weChats = dataObj.data;
                            layui.each(weChats, function (index, item) {
                                var str = buildWeChat(item);
                                var wObj = $('#w_' + item.id);
                                var wHtml = wObj.html();
                                if (wHtml) {
                                    wObj.remove();
                                    $('#LAY_wechat_list').first().prepend(str);
                                } else {
                                    lis.push(str);
                                }
                            });
                            next(lis.join(''), page < dataObj.pages);

                            $(".layui-side-wechat").click(function () {
                                var wechatObj = $(this);
                                if ($(".layui-tab-title li[lay-id]").length <= 0) {
                                    active.tabAdd(
                                        wechatObj.attr("data-name"),
                                        wechatObj.attr("data-id"),
                                        wechatObj.attr("device_ip"),
                                        wechatObj.attr("data-wxid")
                                    );
                                } else {
                                    var isData = false;
                                    $.each($(".layui-tab-title li[lay-id]"), function () {
                                        if ($(this).attr("lay-id") == wechatObj.attr("data-id")) {
                                            isData = true;
                                        }
                                    });
                                    if (isData == false) {
                                        active.tabAdd(
                                            wechatObj.attr("data-name"),
                                            wechatObj.attr("data-id"),
                                            wechatObj.attr("device_ip"),
                                            wechatObj.attr("data-wxid")
                                        );
                                    }
                                }
                                active.tabChange(wechatObj.attr("data-id"));
                            });
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    });
                }
            });
        });
    };

    //取消置顶
    cancel_right_click = function (id) {
        window.document.oncontextmenu = function(){
            return false;
        }
        $('#w_'+id).removeClass('right_click_color')
        $.ajax({
            type: "POST",
            url: "set_top",
            data: {id:id,is_top:1},
            success: function (res) {

            },
        });
        return false;
    }

    //右击菜单 置顶
    right_click = function (id) {
        window.document.oncontextmenu = function(){
            return false;
        }
        var getId = document.getElementById('w_'+id);

        var is_top = getId.getAttribute("data-top");
        if (is_top == 1){
            getId.setAttribute("data-top",2);
            var clone = $('#w_'+id).clone(true);
            $('#w_'+id).remove();
            $('#LAY_wechat_list').prepend(clone);
            $('#w_'+id).addClass('right_click_color')
            $.ajax({
                type: "POST",
                url: "set_top",
                data: {id:id,is_top:2},
                success: function (res) {

                },

            });
        }else{
            $('#w_'+id).removeClass('right_click_color')
            getId.setAttribute("data-top",1);
            $.ajax({
                type: "POST",
                url: "set_top",
                data: {id:id,is_top:1},
                success: function (res) {

                },
            });
        }

        //obj.preventDefault();
        // console.log('右击')
        // console.log()
        return false;
    }

    getSingerWeChats = function (weChatId, friendId, notify) {//已改成流加载
        var lis = [];
        var post = {
            page: 1,
            limit: 20,
            weChatId: weChatId
        };
        $.post('get_wechats_ajax', post, function (dataObj) {
            //假设你的列表返回在data集合中
            if (dataObj.code === 0) {
                var weChats = dataObj.data;
                layui.each(weChats, function (index, item) {
                    // var str = buildWeChat(item);
                    // $('#LAY_wechat_list').first().prepend(str);
                    var weChatList = $('#LAY_wechat_list');
                    var weChatNav = weChatList.find("a[data-id=" + item.id + "]");
                    var weChatDot = weChatNav.find('.layui-badge');
                    if (weChatDot) {
                        weChatDot.remove();
                        if (item.unread_msg_count > 0) {
                            weChatNav.append('<span class="layui-badge" style="position: absolute;right:1px;z-index: 999999;">' + item.unread_msg_count + '</span>');
                            var clone = $('#w_'+item.id).clone(true);
                            $('#w_'+item.id).remove();
                            $('#LAY_wechat_list').prepend(clone);
                        }
                    }
                });

                // $(".layui-side-wechat").click(function () {
                //     var wechatObj = $(this);
                //     if ($(".layui-tab-title li[lay-id]").length <= 0) {
                //         active.tabAdd(wechatObj.attr("data-name"), wechatObj.attr("data-id"));
                //     } else {
                //         var isData = false;
                //         $.each($(".layui-tab-title li[lay-id]"), function () {
                //             if ($(this).attr("lay-id") == wechatObj.attr("data-id")) {
                //                 isData = true;
                //             }
                //         });
                //         if (isData == false) {
                //             active.tabAdd(wechatObj.attr("data-name"), wechatObj.attr("data-id"));
                //         }
                //     }
                //     active.tabChange(wechatObj.attr("data-id"));
                // });
            } else {
                layer.msg(dataObj.msg, {icon: 5});
            }
        });
    };


    var chats;
    getChats = function (boardId, rebuild, friendId) {
        if (rebuild == true) {
            rebuildChatList(boardId);
        }
        layui.use('flow', function () {
            var flow = layui.flow;
            var element = layui.element;
            element.init();

            flow.load({
                elem: '#wechat_chat_list_' + boardId //指定列表容器
                , scrollElem: '.wechat_chat_list'
                , done: function (page, next) { //到达临界点（默认滚动触发），触发下一页
                    var lis = [];
                    var obj = $('#board' + boardId).find('input[name=search_chat]');
                    var search_chat = obj.val();
                    var post = {
                        search: encodeURIComponent(search_chat),
                        page: page,
                        limit: 30,
                        weChatId:boardId
                    };

                    $.post('/cs_work/get_chats_ajax', post, function (res) {
                        //假设你的列表返回在data集合中
                        console.log('getChats');
                        console.log('--------');
                        var dataObj = $.parseJSON(res);
                        if (dataObj.code === 0) {
                            chats = dataObj.data;
                            layui.each(chats, function (index, item) {
                                var str = parserChat(item);
                                lis.push(str);
                            });
                            next(lis.join(''), page < dataObj.pages);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    });
                }
            });
        });

        if (friendId > 0) {
            addNewChat(boardId, friendId);
        }
    };

    var addNewChat = function (boardId, friendId, notify, rebuild) {
        var post = {
            search: '',
            page: 1,
            limit: 1,
            weChatId:boardId,
            friendId:friendId,
        };
        console.log('addNewChat');
        console.log('-------');
        $.ajax({
            type: "POST",
            url: "/cs_work/get_chats_ajax",
            data: post,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    chats = dataObj.data;
                    var board_html = '';
                    var obj = $('#board' + boardId).find('.wechat_chat_list');
                    layui.each(chats, function (index, item) {
                        board_html = parserChat(item);
                        //移除原来的记录再插入
                        if (board_html && board_html != '') {
                            if (notify == true || rebuild == true) {
                                obj.find('div[id=friend' + friendId + ']').remove();
                                obj.first().prepend(board_html);
                            }
                            if (notify == true) {
                                console.log('showDot')
                                showDot(true, boardId, friendId, item.unread_msg_count, dataObj.wechat_unread_msg_count);
                            }
                        }
                    });
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var parserChat = function (item) {
        // return '<div class="layui-row layui-col-space5" style="margin:1px;background: #ffffff;" id="friend' + item.friend_id + '" onclick="showChatRecords(' + item.wechat_id + ', ' + item.friend_id + ', \'' + item.friend_name + '\', ' + item.friend_type + ', \'' + item.friend_remark + '\')"><div class="layui-col-sm3"><img src="' + (item.friend_head_img_url ? item.friend_head_img_url : '/static/cs/images/default_head.jpeg') + '" style="width: 100%; height: 100%;"></div><div class="layui-col-sm9" style="height: 100%;"><span style="float: left;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;">' + (item.friend_name != '' ? item.friend_name : item.friend_username) + '</span><span style="position: relative;float: right;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;">' + item.send_date.replace(/-/g, '/').substr(2, 8) + '</span><span class="layui-form-mid layui-word-aux" style="width:90%;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;">' + (item.content != '' ? item.content : '') + '</span></div><span class="layui-badge" style="' + (item.unread_msg_count > 0 ? '' : 'display:none;') + 'position: absolute;right:1px;z-index: 999999;">' + item.unread_msg_count + '</span></div>';
        return '<div class="layui-row layui-col-space5" style="margin:1px;background: #ffffff;" id="friend' + item.friend_id + '" onclick="showChatRecords(' + item.wechat_id + ', ' + item.friend_id + ', \'' + item.friend_name + '\', ' + item.friend_type + ', \'' + item.friend_remark + '\')"><div class="layui-col-sm3"><img src="' + (item.friend_head_img_url ? item.friend_head_img_url : '/static/cs/images/default_head.jpeg') + '" style="width: 100%; height: 100%;"></div><div class="layui-col-sm9" style="height: 100%;"><span style="float: left;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;">' + (item.friend_name != '' ? item.friend_name : item.friend_username) + '</span><span style="position: relative;float: right;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;color: forestgreen;">' + item.send_date+ '</span><span class="layui-form-mid layui-word-aux" style="width:90%;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;">' + (item.content != '' ? item.content : '') + '</span></div><span class="layui-badge" style="' + (item.unread_msg_count > 0 ? '' : 'display:none;') + 'position: absolute;right:1px;z-index: 999999;">' + item.unread_msg_count + '</span></div>';
    };

    getFriends = function (boardId, click) {//已改成流加载
        if (click == true) {
            rebuildFriendList(boardId);
        }
        layui.use('flow', function () {
            var flow = layui.flow;
            var element = layui.element;
            element.init();

            flow.load({
                elem: '#wechat_friend_list_' + boardId //指定列表容器
                , scrollElem: '.wechat_friend_list'
                , done: function (page, next) { //到达临界点（默认滚动触发），触发下一页
                    var lis = [];
                    var obj = $('#board' + boardId).find('input[name=search_friend]');
                    var search_friend = obj.val();
                    var post = {
                        search: encodeURIComponent(search_friend),
                        page: page,
                        limit: 10,
                        weChatId:boardId
                    };

                    $.post('/cs_work/get_friends_ajax/' + boardId, post, function (res) {
                        //假设你的列表返回在data集合中
                        var dataObj = $.parseJSON(res);
                        if (dataObj.code === 0) {
                            friends = dataObj.data;
                            layui.each(friends, function (index, item) {
                                var str = '<div class="layui-row layui-col-space5" style="margin:1px;background: #f9f9f9;" id="' + item.id + '" onclick="getFriendInfo(' + boardId + ', ' + item.id + ')"><div class="layui-col-sm3"><img src="' + (item.head_img_url ? item.head_img_url : '/static/cs/images/default_head.jpeg') + '" style="width: 100%; height: 100%;"></div><div class="layui-col-sm9"><span>' + (item.remark ? item.remark : item.nickname) + '</span></div></div>';
                                lis.push(str);
                            });
                            next(lis.join(''), page < dataObj.pages);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    });
                }
            });
        });
    };

    requestSyncFriends = function (weChatId) {
        $.ajax({
            type: "GET",
            url: "/cs_work/newFriendsTask?weChatId=" + weChatId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    layer.msg(dataObj.msg, {icon: 1});
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    getChatRecord = function (wechatId, friendId, Old) {
        var lastId = 0;
        var obj = $('#friendChat_' + wechatId + '_' + friendId).find('.layim-chat-main');
        obj.find('.load-more-message').css('display', 'none');
        obj.find('.loading-more-message').css('display', 'block');
        if (Old == true) {
            var ulObj = obj.find('ul');
            var first = ulObj.find('li').first();
            if (first.is('li')) {
                // console.log(first.html());
                lastId = first.attr('id');
                lastId = lastId.replace('record_', '');
                lastId = Number(lastId);
                // console.log('Old recordId:'+lastId);
            }
        }
        var post = {
            lastId: lastId,
            wechatId: wechatId,
            friendId: friendId,
        };
        $.ajax({
            type: "POST",
            data: post,
            url: "/cs_work/get_chat_record_ajax",
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var msgs = dataObj.data;
                    if (msgs.length > 0) {
                        $.each(msgs, function (i, msg) {
                            new_msg(msg);
                        });
                    } else {
                        var noMoreMsg = '没有更多记录了';
                        obj.find('.layui-flow-more').html(noMoreMsg);
                    }
                    obj.find('.load-more-message').css('display', 'block');
                    obj.find('.loading-more-message').css('display', 'none');
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                    obj.find('.load-more-message').css('display', 'block');
                    obj.find('.loading-more-message').css('display', 'none');
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
                obj.find('.load-more-message').css('display', 'block');
                obj.find('.loading-more-message').css('display', 'none');
            }
        });
    };

    getFriendInfo = function (wechatId, friendId) {
        syncFriendInfo(wechatId, friendId);
        $.ajax({
            type: "GET",
            data: {wechatId:wechatId,friendId:friendId},
            url: "/cs_work/get_friend_info_ajax/",
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var friendInfo = dataObj.data;
                    showFriendInfo(wechatId, friendId, friendInfo);
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var syncFriendInfo = function (wechatId, friendId) {
        $.ajax({
            type: "GET",
            url: "/cs_work/newFriendInfoTask/" + wechatId + "/" + friendId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {

                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                // layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    showChatRecords = function (wechatId, friendId, friendName, friendType, rebuildChat, friendRemark) {
        var boardObj = $('#board' + wechatId);
        var charRecord = $('#friendChat_' + wechatId + '_' + friendId);
        if (charRecord.is('div')) {

        } else {
            var board_html = '';
            var getTpl = tpl_chat_records.innerHTML;
            var data = {
                "friend_name": friendName,
                'friend_id': friendId,
                'wechat_id': wechatId,
                'friend_remark': friendRemark
            };
            laytpl(getTpl).render(data, function (html) {
                board_html = $.trim(html);
            });
            var obj = boardObj.find('.layim-chat-box');
            obj.html(board_html);
            freshChartRecords(wechatId, friendId);

            var height = $('#LAY_wechat_content').height();
            var chatMainHeight = (height - 60 - 21 - 20 - 38 - 174 - 38 - 1 + 15 + 10);
            $('#friendChatRecord_' + wechatId + '_' + friendId).height(chatMainHeight);
            // addNewChat(wechatId, friendId, false, rebuildChat);
        }
        showDot(false, wechatId, friendId);
        hotkeySend(wechatId, friendId);
        // requestFriendSnsPage(wechatId, friendId);
        // getFriendSnsPages(wechatId, friendId);
        getCustomerInfo(wechatId, friendId);
        getFriendTags(wechatId, friendId);
        getFriendInfo(wechatId, friendId);
        showMoreWindow(wechatId, friendType);
        // getMaterialGroups(wechatId, friendId);
        showSendImg(wechatId, friendId);
        wholeWeChatId = wechatId;
        wholefriendId = friendId;

        var snsTab = boardObj.find('li[name=snsTab]');
        snsTab.attr('friend_id', friendId);
        var materialTab = boardObj.find('li[name=materialTab]');
        materialTab.attr('friend_id', friendId);
    };

    showSnsTabContent = function (wechatId) {
        var snsTab = $('#snsTab_' + wechatId);
        var friendId = snsTab.attr('friend_id');
        console.log('showSnsTabContent:' + wechatId + ',' + friendId);
        requestFriendSnsPage(wechatId, friendId);
        getFriendSnsPages(wechatId, friendId);
    };

    /**
     * 显示快捷标签
     * @param wechatId
     */
        // showMaterialTabContent = function (wechatId) {
        //     var materialTab = $('#materialTab_' + wechatId);
        //     var friendId = materialTab.attr('friend_id');
        //     console.log('showMaterialTabContent:' + wechatId + ',' + friendId);
        //     getMaterialGroups(wechatId, friendId);
        // };

    var showMoreWindow = function (wechatId, friendType) {
            var moreWindowObj = $('#board' + wechatId).find('.wechat_board_right_more_window');
            // if (friendType == 2) {
            moreWindowObj.css('display', 'block');
            // } else {
            //     moreWindowObj.css('display', 'none');
            // }
        };

    var freshChartRecords = function (wechatId, friendId) {
        getChatRecord(wechatId, friendId);
    };

    showFriendInfo = function (wechatId, friendId, friendInfo) {
        var board_html = '';
        var getTpl = tpl_friend_info.innerHTML;
        var data = {'friend_id': friendId, 'wechat_id': wechatId, 'friendInfo': friendInfo};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#board' + wechatId).find('.layim-friend-info');
        obj.html(board_html);
    };

    sendMsgToFriend = function (wechatId, friendId, friendName, friendRemark, friendType) {
        friendRemark = $('#friend_remark').html();
        showChatWindow('board' + wechatId, wechatId, false, friendId, friendRemark);
        showChatRecords(wechatId, friendId, friendName, friendType, true, friendRemark);
    };

    deleteFriend = function (wechatId, friendId, friendName) {
        layer.confirm('您确定要删除好友 ' + friendName + ' ？', {
            btn: ['确定删除', '取消'] //按钮
        }, function () {
            $.ajax({
                type: "GET",
                url: "/cs_work/newDeleteFriendTask/" + wechatId + "/" + friendId,
                success: function (response) {
                    var dataObj = $.parseJSON(response);
                    if (dataObj.code === 0) {
                        layer.msg('删除请求已提交', {icon: 1});
                    } else {
                        layer.msg(dataObj.msg, {icon: 5});
                    }
                },
                error: function (request, status, error) {
                    layer.msg('哦噢，网络开小差了', {icon: 5});
                }
            });
        }, function () {
//                layer.msg('待完善', {
//                    time: 20000, //20s后自动关闭
//                    btn: ['明白了', '知道了']
//                });
        });
    };

    getStrangers = function (wechatId) {
//            var obj = $('#board' + wechatId).find('input[name=search_friend]');
//            var search_friend = obj.val();
        var post = {
//                search: encodeURIComponent(search_friend),
            wechatId:wechatId,
            page: 1,
            limit: 1000
        };
        $.ajax({
            type: "POST",
            url: "/cs_work/get_strangers_ajax",
            data: post,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var strangers = dataObj.data;
                    freshStrangers(strangers, wechatId);
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var freshStrangers = function (strangers, wechatId) {
        var board_html = '';
        var getTpl = tpl_stranger_list.innerHTML;
        var data = {"list": strangers, 'wechat_id': wechatId};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#board' + wechatId).find('.wechat_stranger_list');
        if (board_html && board_html != '') {
            obj.html(board_html);
        } else {
            obj.html('');
        }
    };

    getStrangerInfo = function (wechatId, strangerId) {
        showStrangerItemDot(false, strangerId);
        showStrangerDot(false, wechatId);
        showStrangerTabDot(false, wechatId);
        $.ajax({
            type: "GET",
            url: "/cs_work/get_stranger_info_ajax?wechatId=" + wechatId + "&strangerId=" + strangerId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var strangerInfo = dataObj.data;
                    showStrangerInfo(wechatId, strangerId, strangerInfo);
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    showStrangerInfo = function (wechatId, strangerId, strangerInfo) {
        var board_html = '';
        var getTpl = tpl_stranger_info.innerHTML;
        var data = {'id': strangerId, 'wechat_id': wechatId, 'strangerInfo': strangerInfo};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#board' + wechatId).find('.layim-friend-info');
        obj.html(board_html);
    };

    acceptStranger = function (strangerId) {
        $.ajax({
            type: "GET",
            url: "/cs_work/newAcceptFriendTask/" + strangerId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    layer.msg('通过请求已提交', {icon: 1});
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    replyStranger = function (wechatId, strangerId) {
        var board_html = '';
        var getTpl = tpl_reply_stranger.innerHTML;
        var data = {'stranger_id': strangerId};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        layer.open({
            title: '回复好友验证申请'
            , type: 1
            , area: '300px'
            //,skin: 'layui-layer-rim'
            , shadeClose: true
            , content: board_html
            , btn: ['确定回复', '取消']
            , yes: function (index, layero) {
                var idObj = layero.find('input[name=stranger_id]');
                var stranger_id = idObj.val();
                var replyObj = layero.find('textarea[name=reply_stranger]');
                var replyContent = replyObj.val();
                if (replyContent && replyContent.length > 0) {
                    if (replyContent.length > 50) {
                        layer.msg('验证内容不能超过50个字', {icon: 5});
                        return false;
                    }
                    var post = {
                        replyContent: encodeURIComponent(replyContent),
                        stranger_id: stranger_id
                    };
                    $.ajax({
                        type: "POST",
                        url: "/cs_work/newAcceptFriendTask",
                        data: post,
                        success: function (response) {
                            var dataObj = $.parseJSON(response);
                            if (dataObj.code === 0) {
                                layer.msg('回复已发送', {icon: 1});
                                layer.close(index);
                                getStrangerInfo(wechatId, strangerId);
                            } else {
                                layer.msg(dataObj.msg, {icon: 5});
                            }
                        },
                        error: function (request, status, error) {
                            layer.msg('哦噢，网络开小差了', {icon: 5});
                        }
                    });
                } else {
                    layer.msg('请输入回复内容', {icon: 5});
                    return false;
                }
            }
            , btn2: function (index, layero) {

            }
        });
    };

    showAddFriend = function (wechatId) {
        var board_html = '';
        var getTpl = tpl_add_friend.innerHTML;
        var data = {'wechat_id': wechatId};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        layer.open({
            title: '加好友'
            , type: 1
            , area: '300px'
            //,skin: 'layui-layer-rim'
            , shadeClose: true
            , content: board_html
            , btn: ['发送', '取消']
            , yes: function (index, layero) {
                var idObj = layero.find('input[name=wechat_id]');
                var wechat_id = idObj.val();
                var searchObj = layero.find('input[name=search_stranger]');
                var search = searchObj.val();
                var msgObj = layero.find('textarea[name=friend_msg]');
                var friendMsg = msgObj.val();

                if (search && search.length > 0) {

                } else {
                    layer.msg('请输入手机号、微信号或QQ号', {icon: 5});
                    return false;
                }
                if (friendMsg && friendMsg.length > 0) {
                    if (friendMsg.length > 50) {
                        layer.msg('验证内容不能超过50个中文，100个字符', {icon: 5});
                        return false;
                    }
                    var post = {
                        id: wechat_id,
                        search: search,
                        friendMsg: encodeURIComponent(friendMsg)
                    };
                    $.ajax({
                        type: "POST",
                        url: "/cs_work/newSearchContactTask/",
                        data: post,
                        success: function (response) {
                            var dataObj = $.parseJSON(response);
                            if (dataObj.code === 0) {
                                layer.msg('好友验证申请已发送', {icon: 1});
                                layer.close(index);
                            } else {
                                layer.msg(dataObj.msg, {icon: 5});
                            }
                        },
                        error: function (request, status, error) {
                            layer.msg('哦噢，网络开小差了', {icon: 5});
                        }
                    });
                } else {
                    layer.msg('请输入回复内容', {icon: 5});
                    return false;
                }
            }
            , btn2: function (index, layero) {

            }
        });
    };

    friendRemark = function (wechatId, friendId) {
        var board_html = '';
        var getTpl = tpl_friend_remark.innerHTML;
        var data = {'wechat_id': wechatId, 'friend_id': friendId};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        layer.open({
            title: '好友备注'
            , type: 1
            , area: '300px'
            //,skin: 'layui-layer-rim'
            , shadeClose: true
            , content: board_html
            , btn: ['确定', '取消']
            , yes: function (index, layero) {
                var friendRemarkObj = layero.find('input[name=friend_remark]');
                var friendRemark = friendRemarkObj.val();
                var wechatIdObj = layero.find('input[name=wechat_id]');
                var wechatId = wechatIdObj.val();
                var friendIdObj = layero.find('input[name=friend_id]');
                var friendId = friendIdObj.val();

                var post = {
                    wechat_id: wechatId,
                    friend_id: friendId,
                    friend_remark: encodeURIComponent(friendRemark)
                };
                $.ajax({
                    type: "POST",
                    url: "/cs_work/friendRemark/",
                    data: post,
                    success: function (response) {
                        var dataObj = $.parseJSON(response);
                        if (dataObj.code === 0) {
                            $('#friend_remark').html(friendRemark);
                            layer.msg('备注添加成功', {icon: 1});
                            layer.close(index);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    },
                    error: function (request, status, error) {
                        layer.msg('哦噢，网络开小差了', {icon: 5});
                    }
                });
            }
            , btn2: function (index, layero) {

            }
        });
    };

    showEmojiPanel = function (wechatId, friendId) {
        var board_html = '';
        var getTpl = tpl_emoji.innerHTML;
        var data = {'wechat_id': wechatId, 'friend_id': friendId};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var emojiLay = layer.open({
            title: ''
            , type: 1
            , area: ['450px']
            , closeBtn: 0
            , shadeClose: true
            , content: board_html
        });

        $(".face").click(function () {
            var faceText = '';
            var faceObj = $(this);
            var faceType = faceObj.attr('type');
            if (faceType == 'qq') {
                faceText = '[' + faceObj.attr('title') + ']';
            } else if (faceType == 'emoji') {

            }
            var emojiPanel = faceObj.parent().parent().parent();
            if (faceText != '') {
                var thisPanelId = emojiPanel.attr('id');
                var current = $('#' + (thisPanelId.replace('friendChatEmoji_', 'friendChat_')));
                var chatBoxObj = current.find('.new-chat-message');
                // var chatBoxObj = $('#');
                var newChatText = chatBoxObj.val() + faceText;
                chatBoxObj.val(newChatText);
                layer.close(emojiLay);
                chatBoxObj.focus();
            }
        });
    };

    var getMediaLayer;
    getMedia = function (weChatId, recordId, type, imgId) {
        if (imgId > 0) {
            var midimg = $('#chatImg' + imgId).attr('midimg');
            if (midimg == 1) return;
        } else {
            getMediaLayer = layer.msg('正在获取...', {
                shadeClose: false
                , icon: 16
                , shade: 0.01
            });
        }
        $.ajax({
            type: "GET",
            url: '/cs_work/getMedia/' + weChatId + '/' + recordId + '/' + type,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    checkingDownloadStatus = false;
                    if (type == 'EMOTICON') {
                        var emoticonUrl = dataObj.emoticonUrl;
                        var imgObj = $('#chatImg' + imgId);
                        imgObj.attr('src', emoticonUrl);
                    } else {
                        setTimeout(function () {
                            checkDownloadStatus(weChatId, recordId, type, imgId);
                        }, 1000);
                    }
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var checkDownloadStatus = function (weChatId, recordId, type, imgId) {
        if (imgId <= 0 && checkingDownloadStatus) return;
        checkingDownloadStatus = true;
        $.ajax({
            type: "GET",
            url: '/cs_work/checkDownloadStatus/' + weChatId + '/' + recordId + '/' + type,
            success: function (response) {
                layer.close(getMediaLayer);
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var imgWidth = 200;
                    switch (type) {
                        case 'THUMB':
                            imgWidth = 100;
                        case 'MIDIMG':
                        case 'HDIMG':
                            if (imgId > 0) {
                                var imgObj = $('#chatImg' + imgId);
                                imgObj.attr('src', '/cs_work/downloadMedia/' + weChatId + '/' + recordId + '/' + type);
                                imgObj.attr('midimg', '1');
                                imgObj.attr('width', imgWidth + 'px');
                            } else {
                                var json = '{"code":0,"msg":"","title":"浏览原图","id":1,"start":0,"data":[{"alt":"浏览原图","src":"' + '/cs_work/downloadMedia/' + weChatId + '/' + recordId + '/' + type + '","thumb":""}]}';
                                layer.photos({
                                    photos: $.parseJSON(json) //格式见API文档手册页
                                });
                            }
                            break;
                        case 'VIDEO':
                            var t = layer;
                            var playVideo;
                            var src = '/cs_work/downloadMedia/' + weChatId + '/' + recordId + '/' + type
                                , e = document.createElement("video");
                            return e.play ? (t.close(playVideo),
                                void (playVideo = t.open({
                                    type: 1,
                                    title: "播放视频",
                                    area: ["340px", "500px"],
                                    maxmin: !0,
                                    shade: !1,
                                    content: '<div style="background-color: #000; height: 100%;"><video style="position: absolute; width: 100%; height: 100%;" src="' + src + '" loop="loop" autoplay="autoplay"></video></div>'
                                }))) : t.msg("您的浏览器不支持video");
                            break;
                        case 'FILE':
                            var href = '/cs_work/downloadMedia/' + weChatId + '/' + recordId + '/' + type;
                            window.open(href, '_blank');
                            break;
                    }
                } else if (dataObj.code === 1) {
                    checkingDownloadStatus = false;
                    setTimeout(function () {
                        checkDownloadStatus(weChatId, recordId, type, imgId);
                    }, 1000);
                } else {
                    checkingDownloadStatus = false;
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.close(getMediaLayer);
                checkingDownloadStatus = false;
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    getMediaV2 = function (imgId, mediaUrl, type, images, index) {
        layer.close(getMediaLayer);
        // console.log('打开图片')
        // console.log(mediaUrl)
        var imgWidth = 200;
        switch (type) {
            case 'THUMB':
                imgWidth = 100;
                break;
            case 'MIDIMG':
            case 'HDIMG':
                var jsonStr = '{"code":0,"msg":"","title":"","id":1,"start":0,"data":[{"alt":"","src":"' + mediaUrl + '","thumb":""}]}';
                if (images) {
                    images = images.split(',');
                    var imageJsonStr = '';
                    layui.each(images, function (index, image) {
                        imageJsonStr += ',{"alt":"","src":"' + image + '","thumb":""}'
                    });
                    if (imageJsonStr != '') {
                        imageJsonStr = imageJsonStr.substr(1);
                        jsonStr = '{"code":0,"msg":"","title":"","id":1,"start":' + index + ',"data":[' + imageJsonStr + ']}';
                    }
                }
                var json = $.parseJSON(jsonStr);
                layer.photos({
                    photos: json, //格式见API文档手册页
                    shift: 5
                });
                break;
            case 'VIDEO':
                var t = layer;
                var playVideo;
                var e = document.createElement("video");
                return e.play ? (t.close(playVideo),
                    void (playVideo = t.open({
                        type: 1,
                        title: "播放视频",
                        area: ["340px", "500px"],
                        maxmin: !0,
                        shade: !1,
                        content: '<div style="background-color: #000; height: 100%;"><video style="position: absolute; width: 100%; height: 100%;" src="' + mediaUrl + '" loop="loop" autoplay="autoplay"></video></div>'
                    }))) : t.msg("您的浏览器不支持video");
            case 'FILE':
                window.open(mediaUrl, '_blank');
                break;
        }
    };

    requestFriendSnsPage = function (weChatId, friendId) {
        $.ajax({
            type: "GET",
            url: '/cs_work/newSnsUserPageTask?wechatId=' + weChatId + '&friendId=' + friendId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {

                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    getFriendSnsPages = function (weChatId, friendId) {//获取好友朋友圈
        var panelObj = $('#friend_sns_page_panel_' + weChatId);
        var winHeight = getWindowHeight();
        var panelHeight = winHeight - 60 - 41 - 10 - 41 - 10 - 10 - 40;
        panelObj.css('height', panelHeight + 'px');

        var listObj = $('#friend_sns_page_' + weChatId);
        listObj.html('');
        layui.use('flow', function () {
            var flow = layui.flow;
            var element = layui.element;
            element.init();

            flow.load({
                elem: '#friend_sns_page_' + weChatId //指定列表容器
                , scrollElem: '#friend_sns_page_panel_' + weChatId
                , end: '已经拉到底了'
                , done: function (page, next) { //到达临界点（默认滚动触发），触发下一页
                    var lis = [];
                    var post = {
                        wechatId: weChatId,
                        friendId: friendId,
                        page: page,
                        limit: 9
                    };

                    $.post('/cs_work/snsListData', post, function (res) {
                        //假设你的列表返回在data集合中
                        var dataObj = $.parseJSON(res);
                        if (dataObj.code === 0) {
                            var rows = dataObj.data;
                            layui.each(rows, function (index, item) {
                                // var item = row.page;
                                // var ContentObject = item.ContentObject;
                                // var contentStyle = ContentObject.contentStyle;
                                var mediasStr = '';
                                // var medias = ContentObject.medias;
                                var str = '<div class="layui-row layui-col-space2">';
                                str += '<div class="snsPageContent">' + parseEmotion(item.content) + '</div>';
                                if (item.type == 1) {//外部内容

                                    mediasStr += '<div class="snsPageMedia layui-row">';
                                    var snsImages = new Array();
                                    layui.each(item.images, function (index, media) {
                                        snsImages.push(media.url);
                                    });
                                    var snsImageIndex = 0;
                                    layui.each(item.images, function (index, media) {
                                        // mediasStr += '<div class="layui-col-md4"><div class=" snsImgbox"><img id="snsImg' + media.mediaId + '" src="/assets/images/spacer.gif" snsImg="0" onload="getSnsMedia(' + weChatId + ', ' + friendId + ', \'' + media.mediaId + '\', \'THUMB\');" onclick="getSnsMedia(' + weChatId + ', ' + friendId + ', \'' + media.mediaId + '\', \'HDIMG\');"></div></div>';
                                        mediasStr += '<div class="layui-col-md4"><div class=" snsImgbox"><img id="snsImg' + media.mediaId + '" src="' + media.url + '" snsImg="0" onclick="getMediaV2(' + weChatId + ', \'' + media.url + '\', \'HDIMG\', \'' + snsImages + '\', ' + snsImageIndex + ');"></div></div>';
                                        snsImageIndex++;
                                    });
                                    str += mediasStr;
                                    str += '</div>';
                                }
                                else if (item.type == 15) {//视频
                                    mediasStr += '<div class="snsPageMedia layui-row">';
                                    layui.each(item.images, function (index, media) {
                                        mediasStr += '<div class="layui-col-md4" style="cursor: pointer;" onclick="viewOuterContent(\'' + media.url + '\');"><img src="' + media.thumb + '" height="80px"><i class="layui-icon layui-icon-video" style="position: absolute; top: 40%; left: 10%;z-index:2;font-size: 20px;color: #fff;"></i></div>';
                                    });
                                    str += mediasStr;
                                    str += '</div>';
                                }
                                // else {
                                //     mediasStr += '<div class="snsPageMedia layui-row">';
                                //     var snsImages = new Array();
                                //     layui.each(medias, function (index, media) {
                                //         snsImages.push(media.url);
                                //     });
                                //     var snsImageIndex = 0;
                                //     layui.each(medias, function (index, media) {
                                //         mediasStr += '<div class="layui-col-md4"><div class=" snsImgbox"><img id="snsImg' + media.mediaId + '" src="' + media.thumb + '" snsImg="0" onclick="getMediaV2(' + weChatId + ', \'' + media.url + '\', \'HDIMG\', \'' + snsImages + '\', ' + snsImageIndex + ');"></div></div>';
                                //         snsImageIndex++;
                                //     });
                                //     str += mediasStr;
                                //     str += '</div>';
                                // }
                                str += '<div class="snsPageTime layui-word-aux">' + item.create_time + '</div>';
                                // var loveStr = '';
                                // var loves = item.loves;
                                // layui.each(loves, function (index, love) {
                                //     loveStr += '&nbsp;&nbsp;<label>' + parseEmotion(love['name']) + '</label>';
                                // });
                                // var replyStr = '';
                                // var replies = item.replies;
                                // layui.each(replies, function (index, reply) {
                                //     replyStr += '<div>' + parseEmotion(reply['name']) + '：' + parseEmotion(reply['content']) + '</div>';
                                // });
                                // loveStr = (loveStr != '' ? '<div class="snsPageLoves"><i class="layui-icon layui-icon-praise"></i>' + loveStr + '</div>' : '');
                                // replyStr = (replyStr != '' ? '<div class="snsPageReplies">' + replyStr + '</div>' : '');
                                // str += (loveStr != '' || replyStr != '' ? '<div class="snsPageInteraction">' + loveStr + (loveStr != '' && replyStr != '' ? '<hr>' : '') + replyStr + '</div>' : '');
                                str += '</div><hr>';
                                lis.push(str);
                            });
                            next(lis.join(''), page < dataObj.pages);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    });
                }
            });
        });
    };

    getSnsMedia = function (weChatId, friendId, fileId, type, recordId) {
        if (type == 'THUMB') {
            var snsImg = $('#snsImg' + fileId + (recordId ? '_' + recordId : '')).attr('snsImg');
            if (snsImg == 1) return;
        }
        $.ajax({
            type: "GET",
            url: '/cs_work/getMediaSns/' + weChatId + '/' + friendId + '/' + fileId + '/' + type,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    checkingSnSDownloadStatus = false;
                    setTimeout(function () {
                        checkSnsMediaDownloadStatus(fileId, type, recordId);
                    }, 1000);
                } else if (dataObj.code === -1) {
                    layer.msg(dataObj.msg, {icon: 5});
                } else {
                    checkingSnSDownloadStatus = false;
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var checkSnsMediaDownloadStatus = function (fileId, type, recordId) {
        // if (imgId <=0 && checkingSnSDownloadStatus) return;
        // checkingSnSDownloadStatus = true;
        $.ajax({
            type: "GET",
            url: '/cs_work/checkDownloadStatusSns/' + fileId + '/' + type,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    switch (type) {
                        case 'THUMB':
                        case 'HDIMG':
                            if (type == 'THUMB') {
                                var imgObj = $('#snsImg' + fileId + (recordId ? '_' + recordId : ''));
                                imgObj.attr('src', '/cs_work/downloadMediaSns/' + fileId + '/' + type);
                                imgObj.attr('snsImg', '1');
                            } else {
                                var json = '{"code":0,"msg":"","title":"浏览原图","id":1,"start":0,"data":[{"alt":"浏览原图","src":"' + '/cs_work/downloadMediaSns/' + fileId + '/' + type + '","thumb":""}]}';
                                layer.photos({
                                    photos: $.parseJSON(json) //格式见API文档手册页
                                });
                            }
                            break;
                    }
                } else if (dataObj.code === 1) {
                    checkingSnSDownloadStatus = false;
                    setTimeout(function () {
                        checkSnsMediaDownloadStatus(fileId, type, recordId);
                    }, 1000);
                } else {
                    checkingSnSDownloadStatus = false;
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                checkingSnSDownloadStatus = false;
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    viewOuterContent = function (url) {
        layer.open({
            title: ''
            , type: 2
            , area: ['500px', '300px']
            , shadeClose: true
            , content: url
        });
    };

    getCustomerInfo = function (weChatId, friendId) {
        var panelObj = $('#customer_info_panel_' + weChatId);
        var winHeight = getWindowHeight();
        var panelHeight = winHeight - 60 - 41 - 10 - 41 - 10 - 10 - 40;
        panelObj.css('height', panelHeight + 'px');
        $.ajax({
            type: "GET",
            url: "/cs_work/getInfoByFriendId?friendId=" + friendId + "&weChatId=" + weChatId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var customerInfo = dataObj.data;
                    showCustomerInfo(weChatId, friendId, customerInfo);
                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    showCustomerInfo = function (wechatId, friendId, customerInfo) {
        var board_html = '';
        var getTpl = tpl_customer_info.innerHTML;
        var data = {'friend_id': friendId, 'wechat_id': wechatId, 'customerInfo': customerInfo};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#board' + wechatId).find('.layim-customer-info');
        obj.html(board_html);
    };

    //Bof -- 标签
    showTagWindow = function (elemId, boardId) {
        var obj = $("#" + elemId);
        obj.find(".wechat_board_right_friends").css("display", "none");
        obj.find(".wechat_board_right_chat").css("display", "none");
        obj.find(".board_swich_chat").css("color", "c2c2c2");
        obj.find(".board_swich_friend").css("color", "#c2c2c2");
        obj.find(".wechat_board_right_tags").css("display", "block");
        obj.find(".board_swich_tag").css("color", "#5FB878");

        var searchObj = $('#board' + boardId).find('input[name=search_tag]');
        searchObj.val('');
        rebuildTagList(boardId);
        getTags(boardId);

        var height = $('#LAY_wechat_content').height();
        var tagListHeight = (height - 42 - 48);
        $(".tag_list").height(tagListHeight + "px");
    };

    var getAvailableTags = function (weChatId,friendId, obj) {
        $.ajax({
            type: "GET",
            url: "/cs_work/getAvailableTags?wechatId="+weChatId+"&friendId=" + friendId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var tags = dataObj.data;
                    if (obj) {
                        showTags(obj, tags);
                    }
                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                // layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var showTags = function (obj, tags) {
        var board_html = '';
        layui.each(tags, function (index, item) {
            board_html += '<input type="checkbox" name="tag_ids[]" title="' + item.name + '" value="' + item.id + '">';
        });
        if (board_html == '') {
            board_html = '<lable class="layui-form-mid">联系管理员添加新标签</lable>';
        }
        var availableTags = obj.find('.availableTags');
        availableTags.html(board_html);
        form.render();
    };

    getFriendTags = function (weChatId, friendId, obj) {
        $.ajax({
            type: "GET",
            url: "/cs_work/getFriendTag?wechatId="+weChatId+"&friendId=" + friendId,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var friendTags = dataObj.data;
                    //console.log('tag_obj');
                    //console.log(obj);
                    if (obj) {
                        showSelectedFriendTags(obj, friendTags);
                    } else {
                        showFriendTags(weChatId, friendId, friendTags);
                    }
                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                // layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    showFriendTags = function (weChatId, friendId, friendTags) {
        var board_html = '';
        var getTpl = tpl_friend_tag.innerHTML;
        var data = {'friend_id': friendId, 'wechat_id': weChatId, 'friendTags': friendTags};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#board' + weChatId).find('.layim-friend-tag');
        obj.html(board_html);
    };

    var showSelectedFriendTags = function (obj, friendTags) {
        var board_html = '';
        layui.each(friendTags, function (index, item) {
            board_html += '<input type="checkbox" name="tag_ids[]" title="' + item.tag_name + '" checked value="' + item.tag_id + '">';
        });
        if (board_html != '') {
            var existTagsBlock = obj.find('div[id=existTagsBlock]');
            existTagsBlock.removeClass('layui-hide');
        }
        board_html += '<button type="button" class="layui-btn layui-btn-sm" onclick="displayAvailableTagsBlock()"><i class="layui-icon layui-icon-add-1"></i></button>';
        var existTags = obj.find('.existTags');
        existTags.html(board_html);
        form.render();
    };

    displayAvailableTagsBlock = function () {
        var availableTagsBlock = $('#availableTagsBlock');
        availableTagsBlock.removeClass('layui-hide');
        var newTagBlock = $('#newTagBlock');
        newTagBlock.removeClass('layui-hide');
    };

    removeTag = function (weChatId, friendId, tagId) {
        layer.confirm('确认删除此标签？', function (index) {
            var post = {
                tag_id: tagId,
                friend_id: friendId,
                wechatId: weChatId
            };
            $.ajax({
                type: "POST",
                url: "/cs_work/removeTag",
                data: post,
                success: function (response) {
                    var dataObj = $.parseJSON(response);
                    if (dataObj.code === 0) {
                        getFriendTags(weChatId, friendId);
                    } else {
                        layer.msg(dataObj.msg, {icon: 5});
                    }
                },
                error: function (request, status, error) {
                    layer.msg('哦噢，网络开小差了', {icon: 5});
                }
            });
            layer.close(index);
        });
    };

    /**
     * 添加文本素材
     * @param weChatId
     * @param friendId
     */
    editMess = function (weChatId, friendId) {
        var board_html = '';
        var getTpl = tpl_add_mess_tag.innerHTML;
        var dataTpl = {};
        laytpl(getTpl).render(dataTpl, function (html) {
            board_html = $.trim(html);
        });
        layer.open({
            title: '添加快捷回复语'
            , type: 1
            , area: ['600px', '350px']
            //,skin: 'layui-layer-rim'
            , shadeClose: true
            , content: board_html
            , btn: ['确定添加', '取消']
            , success: function (layero, index) {
                //getFriendTags(weChatId, friendId, layero);
                //getAvailableTags(friendId, layero);
            }
            , yes: function (index, layero) {
                // var tag_ids = getExistTagIds(layero);
                var titleObj = layero.find('input[name=title]');
                var contentObj = layero.find('textarea[name=mess_content]');
                var title = titleObj.val();
                var content = contentObj.val();
                var post = {
                    type:1,//素材类型 1文字
                    title: title,
                    content: content
                };

                $.ajax({
                    type: "POST",
                    url: "/cs_work/saveMaterial",
                    data: post,
                    success: function (response) {
                        var dataObj = $.parseJSON(response);
                        console.log(dataObj);
                        if (dataObj.code === 0) {
                            layer.msg(dataObj.msg, {icon: 1});
                            layer.close(index);
                            // setTimeout(function () {
                            //     getFriendTags(weChatId, friendId);
                            // }, 1000);
                            parent.$('.ksmessbody').prepend('<tr class="kuaisuTr'+dataObj.id+'"><td>'+title+'</td><td><span class="layui-btn layui-btn-xs " onclick="sendMaterial('+wholeWeChatId+', '+wholefriendId+', '+dataObj.id+')">发送</span> <br><span class="layui-btn layui-btn-xs" style="margin-top:5px" onclick="removeMaterial('+dataObj.id+')">删除</span></td></tr>');

                        } else {
                            layer.msg('添加失败', {icon: 5});
                        }
                    },
                    error: function (request, status, error) {
                        layer.msg('哦噢，网络开小差了', {icon: 5});
                    }
                });
            }
            , btn2: function (index, layero) {

            }
        });
    }

    //删除素材
    removeMaterial = function (id) {
        layer.confirm('确认删除此素材？', function (index) {

            $.ajax({
                type: "POST",
                url: "/cs_work/delMaterial",
                data: {id:id},
                success: function (response) {
                    var dataObj = $.parseJSON(response);
                    if (dataObj.code === 0) {
                        $('.kuaisuTr'+id).remove();
                        layer.msg(dataObj.msg, {icon: 1});
                    } else {
                        layer.msg(dataObj.msg, {icon: 5});
                    }
                },
                error: function (request, status, error) {
                    layer.msg('哦噢，网络开小差了', {icon: 5});
                }
            });
            layer.close(index);
        });
    }


    editTag = function (weChatId, friendId) {
        var board_html = '';
        var getTpl = tpl_add_tag.innerHTML;
        var dataTpl = {};
        laytpl(getTpl).render(dataTpl, function (html) {
            board_html = $.trim(html);
        });
        layer.open({
            title: '设置好友标签'
            , type: 1
            , area: ['600px', '350px']
            //,skin: 'layui-layer-rim'
            , shadeClose: true
            , content: board_html
            , btn: ['确定修改', '取消']
            , success: function (layero, index) {
                getFriendTags(weChatId, friendId, layero);
                getAvailableTags(weChatId,friendId, layero);
            }
            , yes: function (index, layero) {
                var tag_ids = getExistTagIds(layero);
                var newTagNameObj = layero.find('input[name=new_tag_name]');
                var new_tag_name = newTagNameObj.val();
                var post = {
                    friend_id: friendId,
                    wechat_id: weChatId,
                    tag_ids: tag_ids,
                    new_tag_name: encodeURIComponent(new_tag_name)
                };
                $.ajax({
                    type: "POST",
                    url: "/cs_work/saveTag",
                    data: post,
                    success: function (response) {
                        var dataObj = $.parseJSON(response);
                        if (dataObj.code === 0) {
                            layer.msg(dataObj.msg, {icon: 1});
                            layer.close(index);
                            setTimeout(function () {
                                getFriendTags(weChatId, friendId);
                            }, 1000);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    },
                    error: function (request, status, error) {
                        layer.msg('哦噢，网络开小差了', {icon: 5});
                    }
                });
            }
            , btn2: function (index, layero) {

            }
        });
    };

    var getExistTagIds = function (layero) {
        var objs = layero.find('input[type=checkbox]:checked');
        var ids = [];
        $.each(objs, function (index, obj) {
            ids.push(obj.value)
        });
        return ids;
    };

    getTags = function (boardId, click) {//已改成流加载
        if (click == true) {
            rebuildTagList(boardId);
        }
        layui.use(['flow', 'form'], function () {
            var flow = layui.flow;
            var form = layui.form;
            var element = layui.element;
            element.init();

            flow.load({
                elem: '#tag_list_' + boardId //指定列表容器
                , scrollElem: '.tag_list'
                , done: function (page, next) { //到达临界点（默认滚动触发），触发下一页
                    var lis = [];
                    var obj = $('#board' + boardId).find('input[name=search_tag]');
                    var search_friend = obj.val();
                    var post = {
                        search: encodeURIComponent(search_friend),
                        page: page,
                        limit: 20,
                        wechatId:boardId
                    };

                    $.post('/cs_work/getTags', post, function (res) {
                        //假设你的列表返回在data集合中
                        var dataObj = $.parseJSON(res);
                        if (dataObj.code === 0) {
                            var tags = dataObj.data;
                            layui.each(tags, function (index, item) {
                                // var str = '<hr class="layui-bg-gray"><div class="layui-row layui-col-space5" style="margin:1px;background: #f9f9f9;" id="' + item.id + '" title="' + item.name + '" onclick="getTagFriend(' + boardId + ', ' + item.id + ')"><div class="layui-col-sm9" style="float: left;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;"><i class="layui-icon layui-icon-note" style="font-size:18px; color:#5FB878;"></i> <span>' + item.name + '</span></div><div class="layui-col-sm3">(122)</div></div>';

                                var str = '<div class="layui-row layui-col-space10" style="background: #f9f9f9;margin:5px 0 0;border-top-color: #dddddd;border-top-style: solid;border-top-width: 1px;border-bottom-color: #dddddd;" id="tag' + item.id + '" title="' + item.name + '" onclick="getTagFriend(' + boardId + ', ' + item.id + ')"><div class="layui-col-sm9" style="float: left;overflow: hidden;white-space: nowrap;text-overflow: ellipsis;"><i class="layui-icon layui-icon-note" style="font-size:18px; color:#5FB878;"></i> <span>' + item.name + '</span></div><div class="layui-col-sm3">(' + item.num + ')</div></div>';
                                lis.push(str);
                            });
                            next(lis.join(''), page < dataObj.pages);
                        } else {
                            layer.msg(dataObj.msg, {icon: 5});
                        }
                    });
                }
            });
        });
    };

    getTagFriend = function (weChatId, tagId) {
        //执行渲染
        table.render({
            elem: '#tag_friend_table_' + weChatId //指定原始表格元素选择器（推荐id选择器）
            // ,height: 315 //容器高度
            , url: '/cs_work/getTagFriend?wechatId=' + weChatId + '&tagId=' + tagId //数据接口
            , page: true //开启分页
            , cols: [[
                {field: 'id', title: '标签好友', fixed: 'left', templet: '#wxidTpl'}
                , {fixed: 'right', width: 100, align: 'center', toolbar: '#tagFriendBar'}
            ]] //设置表头
            //,…… //更多参数参考右侧目录：基本参数选项
        });
    };
    //Eof -- 标签

    //Bof -- 快捷回复
    getMaterialGroups = function (weChatId, friendId) {
        $.ajax({
            type: "GET",
            url: "/cs_work/materialGroup",
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var materialGroups = dataObj.data;
                    showMaterialGroup(weChatId, friendId, materialGroups);
                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                // layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var showMaterialGroup = function (weChatId, friendId, materialGroups) {
        var board_html = '';
        var getTpl = tpl_material_group.innerHTML;
        var data = {'friend_id': friendId, 'wechat_id': weChatId, 'materialGroups': materialGroups};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#quick_reply_groups_' + weChatId);
        obj.html(board_html);
        element.init();
    };

    getMaterials = function (weChatId, friendId, groupId) {
        $.ajax({
            type: "GET",
            url: "/cs_work/materialListData?groupId="+groupId+"&status=1",
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code === 0) {
                    var materials = dataObj.data;
                    showMaterial(weChatId, friendId, materials);
                } else {
                    // layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {
                // layer.msg('哦噢，网络开小差了', {icon: 5});
            }
        });
    };

    var showMaterial = function (weChatId, friendId, materials) {
        var board_html = '';
        var getTpl = tpl_material.innerHTML;
        var data = {'friend_id': friendId, 'wechat_id': weChatId, 'materials': materials};
        laytpl(getTpl).render(data, function (html) {
            board_html = $.trim(html);
        });
        var obj = $('#quick_reply_' + weChatId);
        obj.html(board_html);
    };

    sendMaterial = function (weChatId, friendId, materialId) {

        // var materialTab = $('#materialTab_' + weChatId);
        // var theFriendId = materialTab.attr('friend_id');
        // if (theFriendId > 0) {
        //     friendId = theFriendId;
        // }
        var post = {
            id: materialId,
            weChatId: wholeWeChatId,
            friendId: wholefriendId
        };
        $.ajax({
            type: "POST",
            url: "/cs_work/materialSend",
            data: post,
            success: function (response) {
                var dataObj = $.parseJSON(response);
                if (dataObj.code == 0) {
                    layer.msg('发送中...', {icon: 1});
                    if (dataObj.record) {
                        var record = dataObj.record;
                        new_msg(record);
                    }
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
            },
            error: function (request, status, error) {

            }
        });
    };
    //Eof -- 快捷回复

    //发送图片
    showSendImg = function (weChatId, friendId) {
        upload.render({
            elem: '#sendImg_' + weChatId + '_' + friendId
            , url: '/cs_work/sendImg/?wechatId=' + weChatId + '&friendId=' + friendId
            , field: 'file_upload_' + weChatId + '_' + friendId
            , accept: 'file' //普通文件
            , exts: 'jpg|jpeg|png' //只允许上传压缩文件
            , size: 1024 * 4 //限制文件大小，单位 KB
            , before: function (obj) {
                layer.load(); //上传loading
            }
            , done: function (res) {
                console.log(res);
                var dataObj = res;//$.parseJSON(res);
                if (dataObj.code == 0) {
                    layer.msg('发送中...', {icon: 1});
                    new_msg(dataObj.record);
                } else {
                    layer.msg(dataObj.msg, {icon: 5});
                }
                layer.closeAll('loading'); //关闭loading
            }
            , error: function (index, upload) {
                console.log('upload error');
                layer.closeAll('loading'); //关闭loading
            }
        });
    };

    //标记消息已读
    setMsgRead = function (weChatId, friendId) {
        var post = {
            weChatId: weChatId,
            friendId: friendId
        };
        $.ajax({
            type: "POST",
            url: "setMsgRead",
            data: post,
            success: function (response) {

            },
            error: function (request, status, error) {

            }
        });
    };

    //快捷键发送
    var hotkeySend = function (wechatId, friendId) {
        var charRecord = $('#friendChat_' + wechatId + '_' + friendId);
        if (charRecord.is('div')) {
            var textarea = charRecord.find('.new-chat-message');
            textarea.focus();
            textarea.off('keydown').on('keydown', function (e) {
                // var local = layui.data('layim')[cache.mine.id] || {};
                var keyCode = e.keyCode;
                // if(local.sendHotKey === 'Ctrl+Enter'){
                //     if(e.ctrlKey && keyCode === 13){
                //         sendMessage();
                //     }
                //     return;
                // }
                if (keyCode === 13) {
                    // if (e.ctrlKey) {
                    //     return textarea.val(textarea.val() + '\n');
                    // }
                    if (e.shiftKey) return;
                    e.preventDefault();
                    sendMsg(wechatId, friendId);
                }
            });
        }
    };

    var getWindowHeight = function () {
        //获取浏览器窗口高度
        var winHeight = 0;
        if (window.innerHeight)
            winHeight = window.innerHeight;
        else if ((document.body) && (document.body.clientHeight))
            winHeight = document.body.clientHeight;
        //通过深入Document内部对body进行检测，获取浏览器窗口高度
        if (document.documentElement && document.documentElement.clientHeight)
            winHeight = document.documentElement.clientHeight;
        return winHeight;
    };

    var autodivheight = function () { //函数：获取尺寸
        var winHeight = getWindowHeight();
        //DIV高度为浏览器窗口的高度
        // var height = (winHeight-60-44-15-41-20-3-25);
        var height = (winHeight - 60 - 44 - 41 - 20 - 2);
        var weChatListHeight = (winHeight - 60 - 45 - 40);
        document.getElementById("LAY_wechat_content").style.height = height + "px";
        document.getElementById("LAY_wechat_list").style.height = weChatListHeight + "px";

        $(".wechat_board_right_chat_friend").height(height + "px");
        $(".wechat_board_right_friend_list").height(height + "px");

        var chatListHeight = (height - 60 - 58);
        $(".wechat_chat_list").height(chatListHeight + "px");
        var strangerListHeight = (height - 42 - 48 - 42 - 42 - 15);
        $(".wechat_stranger_list").height(strangerListHeight + "px");
        var friendListHeight = (height - 42 - 48 - 42 - 42 - 15);
        $(".wechat_friend_list").height(friendListHeight + "px");
        var tagListHeight = (height - 42 - 48);
        $(".tag_list").height(tagListHeight + "px");
    };
    autodivheight();
    window.onresize = autodivheight; //浏览器窗口发生变化时同时变化DIV高度

    getWeChats();
});
