<template>
  <div id="App" >
  <div id="header">
    <div class="left">
      <img class="bird-icon" src="../img/鸟.png">
        <span class="brain">{{base}}</span>
        <div class="container" @mouseover="showMenu = true"  @mouseout="handleGlobalMouseOut">
          <img  @click="showMenu = true"  src="../img/下箭头.png" alt="Image" width="15px" height="15px" >
          <div  class="dropdown-menu"       v-show="showMenu" >
            <div class="dropdown-item" >
              <h4>个人</h4>
              <div class="index-module">
                  <div class="index-module_Pic">
                    <img class="img" src="../img/头像.png">
                  </div>
                <div class="index-module_Desc">
                    <p class="index-module_name">J.12-3.18</p>
                    <p class="index-module_desc">我自己</p>
                </div>
                <div>
                  <img class="check-mark" src="../img/对勾.png">
                </div>
              </div>
              </div>
            <div class="index-module_menu">
              <h4>空间</h4>
              <li class="menu-item-active">
                <a class="hyperlink" href="http://localhost:8081">
                    <p class="index-module_addContent">
                      <img class="add-icon" src="../img/加号.png">
                    </p>
                  <span class="index-module_text">创建空间</span>
                </a>
              </li>
            </div>
          </div>
        </div>


          <div class="smallbell">
            <img @click="showModal=true"  @mouseover="showmessage=true" @mouseout="showmessage=false" src="../img/铃铛.jpg" alt="Image" width="12px" height="12px" style="right:100px"/>
            <div  class="click-bell"
                   v-if="showModal" >
                <span>
                  <el-button style="float: right;margin-right: 20px;margin-top: 15px;" @click="showModal=false">✕</el-button>
                  <div class="message bar">
                    <p style="margin-left: 48px; margin-top: 20px; padding: 0; ">消息中心</p>
                    <div class="mon">
                        <button
                            v-for="(btn, index) in buttons"
                            :key="index"
                            :class="btn.active ? 'active' : ''"
                            @click="selectButton(index)"
                            :style="{ backgroundColor: btn.hover && index !== selectedIndex ? 'lightgray' : 'gray', color: btn.active ? 'black' : 'white', transition: 'background-color 0.3s' }"
                            style="margin-top: 10px; width: 150px;height: 35px;cursor: pointer"
                        >{{ btn.label }}
                        </button>
                    </div>
                    <div class="line" ></div>
                  </div>
                  <div class="module">
                  <button
                     style="border: none; margin-left: 230px; background-color: initial; cursor: pointer"
                     :style="isButtonRead ? { color: '#585A5A' } : { color: 'black' }"
                     @click="toggleButtonColor('未读')">未读</button>

                  <button
                      style="border: none; margin-left: 20px; background-color: initial; cursor: pointer"
                      :style="isButtonRead ? { color: 'black' } : { color: '#585A5A' }"
                      @click="toggleButtonColor('已读')">已读</button>

                  <button
                      style="border: none; margin-left: 270px;color: #585A5A"
                      v-if="!isAllRead"
                    :style="{ backgroundColor: 'initial' }"
                    @click="toggleAllRead">全部已读
                  </button>
                  </div>
                <el-button type="primary" @click="showModal=false"></el-button>
                </span>
            </div>
            <div   class="dropdown-bell"
                   v-if="showmessage" >
              <div class="dropdown-blok">
                <p>{{message}}</p>
              </div>
          </div>
          </div>

      
      <div class="headerUser" @mouseover="showheadsculpture" @mouseleave="checkMouseLeave">
        <div class="index-module_user">
          <div class="index-module_headerUser">
          <img  class="circle" src="../img/头像.png">
          <div class="menu-light" v-show="isshowheadsculpture"  @mouseover="cancelHideMenu" @mouseleave="hideMenu">
            <div class="menu-id">
                  <div class="userInfo">
                    <div class="data-click">
                      <img class="img-avatar" src="../img/头像.png">
                    </div>
                    <div class="badge-module">
                      <span class="badge-module_Name">J.12-3.18</span>
                    </div>
                  </div>
            </div>
            <span class="badge-line"></span>
            <li class="garden">
              <a class="garden-link" href="/j12318" target="_blank">
                <img class="garden-icon" src="../img/分类花瓣.png">
                <span class="text">我的花园</span>
              </a>
            </li>
            <li class="Creativespace">
              <a class="creative-link" href="/j12318" target="_blank">
                <img class="creative-icon" src="../img/创作空间.png">
                <span class="space-text">创作中心</span>
              </a>
            </li>
            <li class="AccountSetting">
              <a class="setting-link" href="/j12318" target="_blank">
                <img class="setting-icon" src="../img/设置.png">
                <span class="setting-text">账户设置</span>
              </a>
            </li>
            <span class="setting-line"></span>
            <div class="Logout">
              <span>
                <img class="logout-icon" src="../img/退出登录.png">
                <span class="Logout-text">退出登录</span>
              </span>
            </div>
            <div class="login-out-menu">
              <span class="index-module_itemAction">
                <div class="switch"  @mouseover="showTooltip = true" @mouseleave="showTooltip = false">
                    <img class="switch-icon" src="../img/中英文切换（英）.png" alt="Language Switch">
                  <div class="tooltip"  v-show="showTooltip">
                    <div class="tooltip-content">
                    <div class="tooltip-arrow">
                      <span class="tooltip-arrow-content"></span>
                  </div>
                  <div class="tooltip-inner">English</div>
              </div>
            </div>
                </div>
              </span>
            </div>
          </div>
          </div>
        </div>
      </div>

      <div class="menu"  style="width: 185px;height: 32px;cursor: pointer" @click="showsearch" >
        <div class="search" style="width: 254px;height: 64px;">
          <span class="search box" >
            <img  src="../img/搜索.png" style=" margin-top:7px;padding-left:5px;position: absolute;height: 18px;width: 18px;"/>
          <input   class="search-icon"    placeholder="搜索                         Ctrl J" />
          </span>
          <div v-if="showPopup" class="search-popup" :style="{ height: popupHeight + 'px'}" @blur="closeSearch">
            <img class="search_icon" src="../img/搜索.png">
            <input type="text" class="search_text"    @input="updateSearch"   v-model="searchText"  placeholder="搜索内容，或输入 > 唤醒更多
                                                                                                     切换内容"/>
            <img class="empty" src="../img/清空&删除&叉叉_面.png" v-if="emptyIcon" @click="closePopup">
            <span class="inputkeys">
              <img class="icon-down" src="../img/下箭头方形.png"  v-if="showIcon">
              <img class="icon-up" src="../img/上箭头方形.png"  v-if="showIcon">
              <li class="search_line"></li>
            </span>
            <div  style="position: absolute;top: 0px;left: 0px;width: 100%">
              <ul class="data-menu-list" v-if="showSearchResults <= 1 && showSearchResults" >
                <li style="list-style: none"><span>页面</span></li>
                   <li class="menu-item"    @mouseover="hoveredIndex  = 0" @mouseleave="hoveredIndex  = null"  :class="{ 'hovered': hoveredIndex  === 0 }">
                     <div>
                       <img class="time-on" src="../img/时间%20开始时间.png">
                       <span class="start">开始</span>
                       <div class="Start-Jump"   v-if="hoveredIndex  === 0 ">
                       <img class="Jump" src="../img/跳转按钮.png">
                       <span class="Jump_text">跳转</span>
                     </div>
                     </div>
                   </li>
                  <li class="menu-item" @mouseover="hoveredIndex  = 1" @mouseleave="hoveredIndex  = null"  :class="{ 'hovered': hoveredIndex  === 1 }">
                    <div>
                      <img class="lark-icon" src="../img/百灵图标.png">
                      <span class="Notes">小记</span>
                      <div class="Notes-Jump" v-if="hoveredIndex  === 1">
                      <img class="Jump" src="../img/跳转按钮.png">
                      <span class="Jump_abel">跳转</span>
                      </div>
                    </div>
                  </li>
                <li class="menu-item-divider"></li>
                <li class="menu-item-text"><span>知识库</span></li>
                <li class="menu-item" @mouseover="hoveredIndex  = 2" @mouseleave="hoveredIndex  = null" :class="{ 'hovered': hoveredIndex  === 2 }">
                  <img class="base-icon" src="../img/知识库.png">
                  <span class="base-default">默认知识库</span>
                  <div class="Base-Jump" v-if="hoveredIndex  === 2">
                  <img class="Jump-icon" src="../img/跳转按钮.png">
                  <span class="Jump-default">跳转</span>
                  </div>
                </li>
              </ul>
            </div>

            <div class="searchbox_text"  v-if="showSearch">
              <ul class="JumpMenu-module">
                <li class="menu-item-child"  @mouseover="hovereditem = 0" @mouseleave="hovereditem = null" :class="{ 'hovered': hovereditem  ===  0}">
                  <div class="jumpItemWrapper" >
                    <span class="jumpItemLabel">在 与个人相关搜索“
                    <b>{{searchText}}</b>
                      ”
                    </span>
                    <span class="JumpMenu"  v-if="hovereditem === 0">
                      <em class="skipicon">↵</em>
                      跳转
                    </span>
                  </div>

                </li>
                <li class="menu-item-public" @mouseover="hovereditem = 1" @mouseleave="hovereditem = null" :class="{ 'hovered': hovereditem  ===  1}">
                  <div class="jumpItem" >
                    <span class="PublicLabel">在 公开知识库搜索“
                    <b>{{searchText}}</b>
                      ”
                    </span>
                    <span class="JumpMenu"  v-if="hovereditem  ===  1">
                      <em class="skipicon">↵</em>
                      跳转
                    </span>
                  </div>
                </li>
                <li class="page" v-if="showStart">
                    <span>页面</span>
                </li>
                <li class="menu-item-start" v-if="showStart" @mouseover="hovereditem = 2" @mouseleave="hovereditem = null" :class="{ 'hovered': hovereditem  ===  2}">
                  <div class="jumpWrapper">
                    <img class="time-icon" src="../img/时间%20开始时间.png">
                    <span class="StartItemLabel"  >开始</span>
                    <span class="StartMenu"   v-if="hovereditem  ===  2">
                      <em class="Start-skipicon">↵</em>
                      跳转
                    </span>
                  </div>
                </li>
                    <div class="extra-content"  v-if="showExtraContent && (hovereditem === 2 || searchText.length > 0)">
                      <span class="Start-divider" v-if="showDivider"></span>
                      <li class="JumpMenu_title"  v-if="showStart">
                          <span>编辑过的文档</span>
                      </li>
                      <li class="Menu_title"  v-if="showStart"  @mouseover="hovereditem = 3" @mouseleave="hovereditem = null" :class="{ 'hovered': hovereditem  ===  3}">
                        <div class="Menu-module">
                          <img class="icon-doc" src="../img/文档管理.png">
                          <span class="document_title">无标题文档</span>
                          <span class="docMenu" v-if="hovereditem  ===  3">
                            <em class="doc-name">J.12-3.18 / 默认知识库</em>
                          </span>
                        </div>
                      </li>
                      <span class="doc-divider" v-if="showDivider"></span>
                      <li class="scan_title"  v-if="showStart">
                        <span>浏览过的文档</span>
                      </li>
                      <li class="Menu_item"  v-if="showStart" @mouseover="hovereditem = 4" @mouseleave="hovereditem = null" :class="{ 'hovered': hovereditem  ===  4}">
                        <div class="document-module">
                          <img class="document-icon" src="../img/文档管理.png">
                          <span class="collect_title">无标题文档</span>
                          <span class="documentMenu" v-if="hovereditem  ===  4">
                            <em class="document-name">J.12-3.18 / 默认知识库</em>
                          </span>
                        </div>
                      </li>
                    </div>
              </ul>
            </div>
          </div>
        </div>
      </div>



          <span class="square"></span>
          <div class="HeadNewButton" >
            <img src="../img/加号.png" @click="showDropdownVisibe" class="showbutton"  @mouseover="isDropdownVisible = true" @mouseout="isDropdownVisible = false"/>
            <div  class="dropdown"  v-show="isDropdownVisible"  @mouseover="isDropdownVisible = true" @mouseout="isDropdownVisible = false">
              <div class="option" @click="handleOptionClick"><img src="../img/文档管理.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">文档</div>
              <div class="option" @click="handleOptionClick"><img src="../img/表格.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">表格</div>
              <div class="option" @click="handleOptionClick"><img src="../img/画板.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">画板</div>
              <div class="option" @click="handleOptionClick"><img src="../img/数据表.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">数据表</div>
              <li class="spilt"></li>
              <div class="option" @click="handleOptionClick"><img src="../img/知识库.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">知识库</div>
              <li class="spilt"></li>
              <div class="option" @click="handleOptionClick"><img src="../img/模板中心.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">从模板新建...</div>
              <div class="option" @click="handleOptionClick"><img src="../img/导入信息.png" style="width: 18px;height: 18px;min-width:18px;margin:5px 12px -3px 8px;">导入</div>
            </div>
            <div class="modal" v-if="isModalVisible">
              <div class="modal-content">
                <div class="ant-modal-close-x">
                <button style="width: 16px;height: 16px;border: none;background-color: initial;font-size: 16px" @click="closeModal">x</button>
                </div>
                  <h3 class="module_title" style="width: 472px;height: 24px">新建数据表</h3>
                  <p class="module_tip" style="width: 472px;height: 22px">选择一个知识库</p>
                  <div class="module_bookSelectorItem" style="width: 472px;height: 49px;">
                      <div class="book-title" style="width: 472px;height: 24px">
                        <span class="book-name">
                        <span>J.12-3.18</span>
                        <span style="margin:0px 4px 0px 4px;line-height: 18.9px">/</span>
                          <span>默认知识库</span>
                        </span>
                        <li class="spilt"></li>
                      </div>
                  </div>
              </div>
            </div>

            <div class="from" v-if="isfromVisible">
              <div class="modal-content">
                <div class="ant-modal-close-x">
                  <button style="width: 16px;height: 16px;border: none;background-color: initial;font-size: 16px" @click="closeModal">x</button>
                </div>
                <h3 class="ftrom_title" style="width: 472px;height: 24px">新建表格</h3>
                <p class="module_tip" style="width: 472px;height: 22px">选择一个知识库</p>
                <div class="module_bookSelectorItem" style="width: 472px;height: 49px;">
                  <div class="book-title" style="width: 472px;height: 24px">
                        <span class="book-name">
                        <span>J.12-3.18</span>
                        <span style="margin:0px 4px 0px 4px;line-height: 18.9px">/</span>
                          <span>默认知识库</span>
                        </span>
                    <li class="spilt"></li>
                  </div>
                </div>
              </div>
            </div>

            <div class="board" v-if="isboardVisible">
              <div class="modal-content">
                <div class="ant-modal-close-x">
                  <button style="width: 16px;height: 16px;border: none;background-color: initial;font-size: 16px" @click="closeModal">x</button>
                </div>
                <h3 class="board_title" style="width: 472px;height: 24px">新建画板</h3>
                <p class="module_tip" style="width: 472px;height: 22px">选择一个知识库</p>
                <div class="module_bookSelectorItem" style="width: 472px;height: 49px;">
                  <div class="book-title" style="width: 472px;height: 24px">
                        <span class="book-name">
                        <span>J.12-3.18</span>
                        <span style="margin:0px 4px 0px 4px;line-height: 18.9px">/</span>
                          <span>默认知识库</span>
                        </span>
                    <li class="spilt"></li>
                  </div>
                </div>
              </div>
            </div>

            <div class="sheet" v-if="issheetVisible">
              <div class="modal-content">
                <div class="ant-modal-close-x">
                  <button style="width: 16px;height: 16px;border: none;background-color: initial;font-size: 16px" @click="closeModal">x</button>
                </div>
                <h3 class="sheet_title" style="width: 472px;height: 24px">新建数据表</h3>
                <p class="module_tip" style="width: 472px;height: 22px">选择一个知识库</p>
                <div class="module_bookSelectorItem" style="width: 472px;height: 49px;">
                  <div class="book-title" style="width: 472px;height: 24px">
                        <span class="book-name">
                        <span>J.12-3.18</span>
                        <span style="margin:0px 4px 0px 4px;line-height: 18.9px">/</span>
                          <span>默认知识库</span>
                        </span>
                    <li class="spilt"></li>
                  </div>
                </div>
              </div>
            </div>

            <div class="base" v-if="isbaseVisible">
              <div class="base-header">
                <div class="base-close-x">
                  <button style="background-color: initial;border: none;cursor: pointer" @click="closeModal">x</button>
                </div>
                <div class="base_title">新建知识库</div>
              </div>
              <div class="base-content">
                    <span class="base_tip">基本信息</span>
                    <div class="popover"></div>
                    <input class="base_input" type="text" v-model="borderinput"  placeholder="知识库名称"/>
                    <textarea class="brief" v-model="briefinput" placeholder="知识库简介（选填）"></textarea>
                    <label class="from-item">新建至</label>
                <div class="selector" @click="toggleBox">
                    <img :style="{ display: showAvatar ? 'block' : 'none' }" class="circle" src="../img/头像.png">
                    <span :style="{ display: showAvatar ? 'block' : 'none' }" class="name-title">J.12-3.18</span>
                    <input class="select" v-model="inputValue" @input="handleInput">
                  <img class="arrow-down" @click="toggleFrame" src="../img/下箭头.png">
                  <div v-if="showBox" >
                    <div class="repeated-element repeated-element-bg">
                    <!-- 在这里放置你想要重复的元素或内容 -->
                   <img class="Avatar-clone"  src="../img/头像.png">
                    <span class="name-clone">J.12-3.18</span>
                    </div>
                    </div>
                </div>
                <div>  <button :disabled="!isReadyToSubmit" class="submitbtn">新建</button></div>
            </div>
            </div>

            <div class="template" v-if="istemplateVisible">
              <div class="template-header">
                <div class="template-close-x">
                  <button style="background-color: initial;border: none;cursor: pointer" @click="closeModal">x</button>
                </div>
                <div class="template_title" style="background-color: #e7e9e8;width: 1000px;height: 300px;text-align: right;">模板中心</div>
              </div>
            </div>

            <div class="import" v-if="isimportVisible">
              <div class="modal-content">
                <div class="ant-modal-close-x">
                  <button style="width: 16px;height: 16px;border: none;background-color: initial;font-size: 16px" @click="closeModal">x</button>
                </div>
                <h3 class="import_title" style="width: 472px;height: 24px">导入</h3>
                <p class="module_tip" style="width: 472px;height: 22px">选择一个知识库</p>
                <div class="module_bookSelectorItem" style="width: 472px;height: 49px;">
                  <div class="book-title" style="width: 472px;height: 24px">
                        <span class="book-name">
                        <span>J.12-3.18</span>
                        <span style="margin:0px 4px 0px 4px;line-height: 18.9px">/</span>
                          <span>默认知识库</span>
                        </span>
                    <li class="spilt"></li>
                  </div>
                </div>
              </div>
          </div>
      </div>
  </div>
  </div>
  <div id="content" >
  </div>
    <div id="footer" >
      </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      base: 'Brain',
      message: '消息中心',
      showMenu: false,  //下箭头显示
      isshowheadsculpture:false, //头像显示
      hideMenuTimeout: null,
      showTooltip: false,
      showmessage: false,
      showModal: false,
      isButtonRead: false, // 表示按钮的当前状态：未读或已读
      isAllRead: false, // 表示是否所有内容都已读，初始为显示全部已读按钮
      lastClickedButton: '', // 跟踪上一次点击的按钮
      buttons: [
        {label: '全部消息', active: false, hover: false},
        {label: '关注', active: false, hover: false},
        {label: '点赞', active: false, hover: false},
        {label: '@和评论', active: false, hover: false},
        {label: '待处理', active: false, hover: false},
        {label: '系统通知', active: false, hover: false},
        {label: '其他消息', active: false, hover: false},
      ],
      selectedIndex: 0, // 当前选中的按钮索引
      showPopup: false, //控制小窗口的显示状态
      isClosing: false,
      searchText: '', // 搜索框的值，可以通过v-model双向绑定数据
      activeIndex: 0, // 当前高亮显示的索引
      hoveredIndex: 0,
      hovereditem: 0,
      //开始，小记，默认知识库，与我相关，公开知识库，页面开始
      hoveredElement: null, hoveredpublic: null, hoveredstart: null, hovereddoc: null, hoveredocument: null,
      showSearchResults: true, // 控制搜索结果的显示和隐藏
      showIcon: true, // 控制图标的显示与隐藏
      emptyIcon: false, //清空图标
      popupHeight: 265, // 初始高度为254px
      showSearch: false,
      showStart: true,
      showDivider: false,
      isDropdownVisible: false, // 控制下拉菜单的显示与隐藏
      dropdownTimeout: null, // 用于延迟隐藏下拉菜单的计时器
      isModalVisible: false, // 控制模态框的显示与隐藏
      isDocumentClicked: false, // 用于控制文档点击后的状态
      showExtraContent: false,
      hasInputBeenUsed: false,
      isfromVisible: false, //表格
      isboardVisible: false, //画板
      issheetVisible: false, //数据表
      isbaseVisible: false, //知识库
      istemplateVisible: false, //从模板新建...
      isimportVisible: false, //导入
      borderinput: '', //知识库输入框
      briefinput: '',   //简介输入框
      showAvatar: true, //知识库头像
      inputValue: '', //头像输入框
      showBox: false, //复制框
    }
  },
  methods: {
    handleGlobalMouseOut(event) {
      // 检查鼠标是否离开了容器及其子元素
      const container = this.$el.querySelector('.container');
      if (!container.contains(event.relatedTarget)) {
        this.showMenu = false;
      }
    },
    showheadsculpture() {
      this.isshowheadsculpture = true;
    },
    checkMouseLeave() {
      // 当鼠标离开 headerUser 时，设置一个定时器来检查鼠标是否离开了页面
      this.hideMenuTimeout = setTimeout(() => {
        this.hideMenu();
      }, 200); // 200 毫秒的延迟，以确保用户没有将鼠标移动到菜单下方
    },
    cancelHideMenu() {
      clearTimeout(this.hideMenuTimeout); // 取消之前的隐藏操作
    },
    hideMenu() {
      this.isshowheadsculpture = false;
    },
  toggleButtonColor(buttonName) {
      if (this.lastClickedButton === buttonName) return; // 如果重复点击同一个按钮，不做任何操作
      this.lastClickedButton = buttonName; // 更新上次点击的按钮为当前按钮
      if (buttonName === '未读') {
        this.isButtonRead = false; // 设置为未读状态和颜色
        this.isAllRead = false; // 隐藏全部已读按钮（如果之前是已读状态）
      } else {
        this.isButtonRead = true; // 设置为已读状态和颜色
        this.isAllRead = true; // 显示全部已读按钮（如果之前是未读状态）
      }
    },
    toggleAllRead() {
      this.isAllRead = !this.isAllRead; // 切换“全部已读”的显示与隐藏状态
    },
    selectButton(index) {
      if (index !== this.selectedIndex) { // 仅当点击的按钮与当前选中按钮不同时，才更新背景颜色
        this.buttons.forEach((btn, i) => (i === index ? (btn.active = true) : (btn.active = false)));
        this.selectedIndex = index;
      }
    },
    handleKeydown(event) {
      // 根据按下的键进行相应的处理，这里仅处理箭头键作为示例
      switch (event.key) {
        case 'ArrowUp': // 上箭头键
          if (this.hoveredIndex > 0) {
            this.hoveredIndex--; // 更新悬停索引为上一个列表项
          } else {
            this.hoveredIndex = this.$el.querySelectorAll('.menu-item').length - 1; // 循环到最后一个列表项
          }
          break;
        case 'ArrowDown': // 下箭头键
          if (this.hoveredIndex < this.$el.querySelectorAll('.menu-item').length - 1) {
            this.hoveredIndex++; // 更新悬停索引为下一个列表项
          } else {
            this.hoveredIndex = 0; // 循环到第一个列表项
          }
          break;
        default:
          break;
      }
      // 只有在处理箭头键时才阻止默认行为
      if (event.key === 'ArrowUp' || event.key === 'ArrowDown') {
        event.preventDefault();
      }
    },
    handleKeyindex(event) {
      // 根据按下的键进行相应的处理，这里仅处理箭头键作为示例
      switch (event.key) {
        case 'ArrowUp': // 上箭头键
          if (this.hovereditem > 0) {
            this.hovereditem--; // 更新悬停索引为上一个列表项
          } else {
            this.hovereditem = this.$el.querySelectorAll('.menu-item-child ,.menu-item-public,.menu-item-start,.Menu_title,.Menu_item').length - 1; // 循环到最后一个列表项
          }
          break;
        case 'ArrowDown': // 下箭头键
          if (this.hovereditem < this.$el.querySelectorAll('.menu-item-child ,.menu-item-public,.menu-item-start,.Menu_title,.Menu_item').length - 1) {
            this.hovereditem++; // 更新悬停索引为下一个列表项
          } else {
            this.hovereditem = 0; // 循环到第一个列表项
          }
          break;
        case 'Enter':
          if (event.key === 'Enter') {
            console.log('Enter 键被按下');
          } else {
            // 可以添加其他键的处理逻辑，如 "Enter" 键等
          }
          break;
          // 可以添加其他键的处理逻辑，如 "Enter" 键等
        default:
          break;
      }
      // 只有在处理箭头键时才阻止默认行为
    },
    resetHoveredItem() {
      // 重置 hovereditem 为第一个项目
      this.hovereditem = 0;
    },
    showsearch() {
      this.showPopup = true;
    },
    showDropdownVisibe(){
      this.isDropdownVisible = true;
    },
    closeSearch() {
      // 关闭弹出窗口的逻辑
      this.showSearchResults = false;
    },
    closePopup() {
      this.searchText = ''; //清空搜索框内容
      this.showSearchResults = true;
      this.showIcon = true;
      this.showSearch = false;
      this.emptyIcon = false;
      this.popupHeight = 254;
    },
    updateSearch() {
      // 根据输入的字符数量来控制显示与隐藏菜单内容
      if (this.searchText.length === 1) {
        if (!this.hasInputBeenUsed) {
          this.hasInputBeenUsed = true;
          this.showExtraContent = false;
        } else {
          // 否则显示额外内容
          this.showExtraContent = true;
          this.showSearch = true;
          this.showStart = true;
          this.showDivider = true;
          setTimeout(() => {
            this.popupHeight = 380; // 高度新增为300px
          }, 10); // 设置计时器的时间，这里设置为10毫秒
        }
        this.showIcon = false; // 隐藏图标
        this.showSearchResults = false; // 隐藏菜单内容
        this.popupHeight = 200; // 高度扩展为391px
        this.showSearch = true;
        this.emptyIcon = true;
        this.showStart = true;
      } else if (this.searchText.length > 1) {
        this.showSearch = true;
        this.showIcon = false; // 显示图标
        this.showSearchResults = false; // 显示菜单内容
        this.popupHeight = 130; // 高度恢复为130px
        this.emptyIcon = true;
        this.showStart = false;
        this.showDivider = false;
      } else {
        this.popupHeight = 254; // 当没有输入时，高度设置为50px（或你想要的任何其他值）
        this.showSearchResults = true; // 显示菜单内容
        this.showSearch = false;
        this.emptyIcon = false;
        this.showIcon = true;
        this.showDivider = false;
        this.showExtraContent = false;
      }
    },
    handleOptionClick(event) {
      if (event.target.textContent === "文档") {
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.isModalVisible = true;
      } else if (event.target.textContent === "表格") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.isfromVisible = true;
      } else if (event.target.textContent === "画板") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.isboardVisible = true;
      } else if (event.target.textContent === "数据表") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.issheetVisible = true;
      } else if (event.target.textContent === "知识库") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.isbaseVisible = true;
      } else if (event.target.textContent === "从模板新建...") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.istemplateVisible = true;
      } else if (event.target.textContent === "导入") {
        // 导航到表格页面或执行其他逻辑
        this.isDocumentClicked = true; // 设置文档点击状态为 true
        this.isDropdownVisible = false; // 收起下拉菜单
        this.isimportVisible = true;
      } else {
        // 设置文档点击状态为 true
      }
    },
    closeModal() {
      this.isModalVisible = false; // 点击关闭按钮时隐藏红色模态框
      this.isfromVisible = false;
      this.isboardVisible = false;
      this.issheetVisible = false;
      this.isbaseVisible = false;
      this.istemplateVisible = false;
      this.isimportVisible = false;
    },
    handleInput() {
      if (this.inputValue.length > 0) {
        this.showAvatar = false; // 当输入框有内容时隐藏头像
      } else {
        this.showAvatar = true; // 当输入框为空时显示头像
      }
    },
    toggleBox() {
      this.showBox = !this.showBox;
    },
  },
  computed: {
    isReadyToSubmit() {
      return this.borderinput || this.briefinput;
    },
  },
  mounted() {
    // 组件挂载后执行的代码
    document.addEventListener('keydown', this.handleKeydown);
    document.addEventListener('keydown', this.handleKeyindex);
  },
  beforeUnmount() {
    // 组件销毁前执行的代码
    document.removeEventListener('keydown', this.handleKeydown);
    document.removeEventListener('keydown', this.handleKeyindex);
  },
  watch: {
    searchText(newValue, oldValue) {
      // 当 searchText 变化时，重置 hovereditem
      if (newValue.length > oldValue.length) {
        // 当输入字符增加时
        this.resetHoveredItem();
      } else if (newValue.length < oldValue.length && newValue.length === 1) {
        // 当输入字符减少到只剩一个时
        this.showExtraContent = true;
      }
    }
  }
}
</script>

<style scoped>
*{
  margin: 0;
  padding: 0;
}
/* 全局 */
#App{
  width: 1205px;
  height: 919px;
}
/* 左侧样式 */
.left{
  background-color: #f5f5f5;
  height: 919px;
  width: 254px;
  top: 0;
  left: 0;
  padding: 10px;
  position: fixed;
}
.bird-icon{
  height: 32px;
  display: block;
  border-style: none;
  box-sizing: border-box;
  line-height: 32px;
}
.brain{
  position: absolute;
  right: 16px;
  top: 1px;
  width: 56px;
  margin-right: 150px;
  align-items: center;
  background-color: transparent;
  flex-direction: row-reverse;
  line-height: 32px;
  margin-top: 10px;
  font-size: 18px;
  font-weight: bold;
}
/*个人知识库*/
span{font-size: 20px;top:20px;cursor: pointer;}
/*箭头图标*/
.container {
  position: absolute;
  top:22px;
  right: 150px;
  cursor: pointer;
}
.container:hover{background-color: #eff0f0;}
/*铃铛图标*/
.smallbell{
  position: absolute;
  top:20px;
  right: 60px;
  z-index: 9999;
}
/*箭头显示*/
.dropdown-menu {
  position: absolute;
  right: -200px;
  top: 100%;
  width: 300px;
  height: 226px;
  padding: 0 20px 12px 20px;
  background-color: #fff; /* 背景颜色 */
  border: 1px solid #e7e9e8;
  border-radius: 8px;
  z-index: 10;
  background-clip: padding-box;
  box-sizing: border-box;
}
/*下拉菜单*/
.dropdown-item {
  display: block;
  padding: 10px;
  margin-right: 0;
  cursor: pointer;
  width: 260px;
  height: 85px;
  color: #262626;
  line-height: 40px;
  font-size: 14px;
  text-align: left;
}
h4{
  margin-top: 16px;
  margin-bottom: 16px;
  font-size: 12px;
  line-height: 17px;
  color: #8a8f8d;
  box-sizing: border-box;
  font-weight: 500;
}
.index-module{
  display: flex;
  padding: 6px 8px;
  border-radius: 6px;
  box-sizing: border-box;
}
.index-module:hover{background-color: #eff0f0;}
.index-module_Pic{
  width: 32px;
  height: 40px;
  display: flex;
  align-items: center;
}
.img{
  width: 32px;
  min-width: 32px;
  height: 32px;
  border-radius: 16px;
  border-color: rgba(0, 0, 0, 0.06);
  border-width: 1px;
  border-style: solid;
}
.index-module_Desc{
  margin-left: 14px;
  width: 168px;
  overflow: hidden;
  display: flex;
  justify-content: center;
  flex-direction: column;
  box-sizing: border-box;
}
.index-module_name{
  display: block;
  line-height: 20px;
  font-size: 14px;
  color: #262626;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-bottom: 0;
  box-sizing: border-box;
  margin-top: 0;
  cursor: pointer;
}
.index-module_desc{
  font-size: 10px;
  line-height: 14px;
  color: #8a8f8d;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  margin-bottom: 0;
  box-sizing: border-box;
  margin-top: 0;
}
.check-mark{
  overflow: hidden;
  display: inline-block;
  color: inherit;
  font-style: normal;
  line-height: 0;
  text-align: center;
  text-transform: none;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
  box-sizing: border-box;
  width: 14px;
  height: 14px;
}
.index-module_menu{
  width: 260px;
  height: 81px;
  box-sizing: border-box;
  display: block;
  padding: 10px;
  margin-right: 0;
  cursor: pointer;
  color: #262626;
  line-height: 40px;
  font-size: 14px;
  text-align: left;
  font-weight: 400;
}
.menu-item-active{
  color: #262626;
  height: auto;
  padding: 0;
  overflow: hidden;
  line-height: 40px;
  text-overflow: ellipsis;
  position: relative;
  display: block;
  margin: 0;
  white-space: nowrap;
  cursor: pointer;
  box-sizing: border-box;
  border-radius: 6px;
  list-style: none;
  width: 260px;
}
.menu-item-active:hover{background-color: #eff0f0;}
.hyperlink{
  color: #262626;
  display: flex;
  align-items: center;
  margin-top: 4px;
  padding: 6px 8px;
  border-radius: 6px;
  box-sizing: border-box;
  transition: opacity .2s ease-in-out;
  cursor: pointer;
  touch-action: manipulation;
  text-decoration: none;
  background-color: transparent;
  outline: none;
}
.index-module_addContent{
  height: 32px;
  border: 1px solid #e7e9e8;
  border-radius: 8px;
  padding: 0 7px;
  background-color: #fff;
  line-height: 32px;
  text-align: center;
  cursor: pointer;
}
.add-icon{
  width: 16px;
  height: 16px;
  display: inline-block;
  font-style: normal;
  line-height: 0;
  text-align: center;
  text-transform: none;
  margin-top: 8px;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
}
.index-module_text{
  margin-left: 14px;
  font-size: 14px;
  line-height: 20px;
  color: #262626;
  box-sizing: border-box;
}
/*铃铛显示*/
.dropdown-bell{
  position: absolute;
  right: -40px;
  top: 100%;
  width: 90px;
  height: 5px;
}
/*铃铛悬浮弹窗*/
.dropdown-blok{
  display: block;
  padding: 10px;
  border: 1px solid #ccc;
  margin-right: 0;
  background-color: #272a27;
  color: white;
  border-radius: 15px;
  text-align: center;
}

/*点击铃铛显示*/
.click-bell{
  display: block;
  background-color: antiquewhite;
  width: 880px;
  height: 610px;
  position: absolute;
  top:110px;
  border-radius: 15px;
}
/*铃铛消息栏*/
.message bar{
  width: 144px;
  height: 610px;
}
/*铃铛实线*/
.line{
  position: absolute;
  left: 180px; /* 调整元素相对于父元素的左侧距离 */
  top: 10px; /* 调整元素相对于父元素的顶部距离 */
  border-left: 1px solid #FFFFFF; /* 设置左边为1像素的黑色实线 */
  height: 595px; /* 设置高度为200像素（根据需要调整） */
}
/*已读头部*/
.module{
  width: 694px;
  height: 52px;
  margin-top: -25px;
}
/*按钮样式*/
.mon{
  text-align:center;position: absolute;margin-top: 20px;padding-top:5px;margin-left:10px;border-radius: 5px;width: 150px;height: 35px;
}
/*头像页面*/
.headerUser {
  width: 36px;
  height: 32px;
  position: absolute;
  margin-left: 220px;
  margin-top: -28px;
  align-self: center;
  box-sizing: border-box;
}
.index-module_user{
  display: flex;
  border-radius: 6px;
  padding: 2px 6px;
  cursor: pointer;
  max-width: 178px;
  align-items: center;
  height: 32px;
  line-height: 25px;
  box-sizing: border-box;
}
.index-module_user:hover{
  background-color: #eff0f0;
}
.index-module_headerUser{
  display: flex;
  align-items: center;
  box-sizing: border-box;
}
.menu{
  position: relative;
}
/*搜索框*/
.search-icon {
  width: 170px;
  height: 32px;
  border-radius: 8px;
  display: block;
  background-color: #FFFFFF;
  border: 1px solid #585A5A;
  margin-top: 30px;
  padding-left: 30px;
  cursor: pointer;
  pointer-events: none;
}
/*搜索布局*/
.search-popup {
  position: fixed; /* 小窗口定位 */
  padding: 15px;
  font-size: 16px;
  line-height: 24px;
  box-shadow: none;
  cursor: pointer;
  background-color: #E1DEDEFF;
  width: 700px;
  height: 265px;
  border-radius: 6px;
  display: inline-block;
  list-style-position: outside;
  margin-left: 280px;
  margin-top: 25px;
}
/*搜索图标*/
.search_icon{
  line-height: 1px;
  font-size: 16px;
  cursor: pointer;
  width: 18px;
  height: 18px;
  margin-right: 16px;
  margin-top: 20px;
}
/*搜索框底纹*/
.search_text{
  position: absolute;
  font-size: 14px;
  width: 660px;
  height: 24px;
  margin-right: 32px;
  padding-left: 2px;
  margin-top: 5px;
  padding-top: 10px;
  padding-bottom: 10px;
  text-align: left;
  box-shadow: none;
  outline: none;
  border: none;
  z-index: 1;
}
/*与我相关搜索*/
.searchbox_text{
  box-sizing: border-box;
  display: block;
  float: none;
  line-height: 22px;
  position: static;
  z-index: auto;
  width: 720px;
  height: 149px;
}
/*与我相关搜索ul层*/
.JumpMenu-module{
  font-size: 14px;
  color: #bec0bf;
  line-height: 22px;
  margin-top: -12px;
  margin-left: -12px;
  width: 703px;
  height: 32px;
  padding-top: 0;
  box-shadow: none;
  background-color: #E1DEDEFF;
}
/*ul层下面的li*/
.menu-item-child{
  width: 687px;
  height: 22px;
  line-height: 22px;
  margin: 4px 8px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  display:flex;
  justify-content: center;
  justify-items: center;
  white-space: nowrap;
  cursor: pointer;
  text-align: left;
  font-size: 14px;
}
.menu-item-child.hovered{background-color: #eff0f0}
.menu-item-public{
  width: 687px;
  height: 22px;
  line-height: 22px;
  margin: 4px 8px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  display:flex;
  justify-content: center;
  justify-items: center;
  white-space: nowrap;
  cursor: pointer;
  text-align: left;
  font-size: 14px;
}
.menu-item-public.hovered{background-color: #eff0f0}
/*搜索框输入开始内容*/
.menu-item-start{
  width: 687px;
  height: 22px;
  line-height: 22px;
  margin: -10px 8px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  display:flex;
  justify-content: center;
  justify-items: center;
  white-space: nowrap;
  cursor: pointer;
  text-align: left;
  font-size: 14px;
}
.menu-item-start.hovered{background-color: #eff0f0}
/*与我相关内容div*/
.jumpItemWrapper{
  display: flex;
  align-items: center;
  position: relative;
  flex-wrap: wrap;
  box-sizing: border-box;
}
/*在 公开知识库搜索*/
.jumpItem{
  display: flex;
  align-items: center;
  position: relative;
  flex-wrap: wrap;
  box-sizing: border-box;
}
/*搜索框输入全局*/
.jumpWrapper{
  display: flex;
  align-items: center;
  position: relative;
  flex-wrap: wrap;
  box-sizing: border-box;
}
/*与我相关内容*/
.jumpItemLabel{
  color: #585a5a;
  width: 525px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: 14px;
  margin-left: -160px;
}
/*搜索框删除全局*/
.extra-content{
  display: flex;
  align-items: center;
  position: absolute;
  flex-wrap: wrap;
  box-sizing: border-box;
  margin-left: 30px}
/*公开知识库内容*/
.PublicLabel{
  color: #585a5a;
  width: 525px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: 14px;
  margin-left: -160px;
}
/*开始*/
.StartItemLabel{
  color: #585A5A;
  width: 525px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  box-sizing: border-box;
  cursor: pointer;
  text-align: left;
  position: absolute;
  margin:-18px 0 -18px -310px;
  font-size: 14px;
  height: 22px;
}
/*开始图标*/
.time-icon{
  width: 18px;
  min-width: 18px;
  height: 18px;
  margin-left: -340px;
  overflow: hidden;
  display: inline-block;
  color: inherit;
  font-style: normal;
  line-height: 0;
  text-align: center;
  white-space: nowrap;
  cursor: pointer;
}
/*开始span*/
.StartMenu{
  display: block;
  position: absolute;
  right: 4px;
  top: 0;
  font-size: 14px;
  cursor: default;
  color: #8a8f8d;
  width: 58px;
  height: 22px ;
  margin: 4px -350px 4px 5px;
}
/*跳转按键*/
.Start-skipicon{
  display: inline-block;
  vertical-align: top;
  font-style: normal;
  margin: -3px 0 -3px 2px;
  position: relative;
  top: 2px;
  border: 1px solid #d8dad9;
  color: #8a8f8d;
  border-radius: 4px;
  width: 18px;
  height: 18px;
  line-height: 18px;
  box-sizing: border-box;
}
/*删除菜单分割线*/
.Start-divider{
  position: absolute;
  width: 730px;
  height: 1px;
  margin: -2px 0;
  padding: 0;
  overflow: hidden;
  line-height: 0;
  background-color: rgba(0,0,0,0.06);
  transform: translateX(-33px)
}
/*编辑过的文档*/
.JumpMenu_title{
  height: 32px;
  line-height: 22px;
  margin: 30px -20px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  outline: none;
  box-shadow: none;
  cursor: default;
  display: block;
  font-size: 14px;
  color: rgb(190,192,191);
  white-space: nowrap;
}
/*编辑过的文档内容样式*/
.Menu_title{
  width: 687px;
  height: 22px;
  line-height: 22px;
  margin: -40px 0 0 -20px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  display:flex;
  justify-content: center;
  justify-items: center;
  white-space: nowrap;
  cursor: pointer;
  text-align: left;
  font-size: 14px;
}
.Menu_title.hovered{
  background-color: #eff0f0;
}
/*编辑过的文档内容div*/
.Menu-module{
  display: flex;
  align-items: center;
  position: relative;
  flex-wrap: wrap;
  color: rgb(38,38,38);
  cursor: pointer;
}
/*编辑过的文档图标*/
.icon-doc{
  width: 18px;
  min-width: 18px;
  height: 18px;
  margin-right: 5px;
  margin-top: 2px;
  text-align: left;
  margin-left: -340px;
  justify-content: center;
  justify-items: center;
  display: inline-block;
  color: inherit;
  font-style: normal;
  line-height: 0;
  text-transform: none;
  text-rendering: optimizeLegibility;
  overflow: hidden;
  white-space: nowrap;
  cursor: pointer;
}
/*无标题文档*/
.document_title{
  color: #585A5A;
  width: 525px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  box-sizing: border-box;
  cursor: pointer;
  text-align: left;
  position: absolute;
  margin:-18px 0 0 -312px;
  font-size: 14px;
  height: 22px;
}
/*文档和id样式*/
.docMenu{
  display: block;
  position: absolute;
  right: 4px;
  top: 0;
  font-size: 14px;
  cursor: default;
  color: #8a8f8d;
  margin: 4px -330px 4px 5px;
  box-sizing: border-box;
  line-height: 22px;
  list-style-position: outside;
  text-align: left;
  white-space: nowrap;
  width: 140px;
  height: 22px;
}
/*文档内容*/
.doc-name{
  display: inline-block;
  vertical-align: top;
  font-style: normal;
  margin: -3px 0 -3px 2px;
  position: relative;
  top: 2px;
  color: #8a8f8d;
  border-radius: 4px;
  line-height: 18px;
  box-sizing: border-box;
}
.doc-divider{
  position: absolute;
  width: 730px;
  height: 1px;
  margin: 85px 0;
  padding: 0;
  overflow: hidden;
  line-height: 0;
  background-color: rgba(0,0,0,0.06);
  transform: translateX(-33px)
}
.scan_title{
  height: 32px;
  line-height: 22px;
  margin: 15px -20px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  outline: none;
  box-shadow: none;
  cursor: default;
  display: block;
  font-size: 14px;
  color: rgb(190,192,191);
  white-space: nowrap;
}
.Menu_item{
  width: 687px;
  height: 22px;
  line-height: 22px;
  margin: -25px 0 0 -20px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  display:flex;
  justify-content: center;
  justify-items: center;
  white-space: nowrap;
  cursor: pointer;
  text-align: left;
  font-size: 14px;
}
.Menu_item.hovered{background-color: #eff0f0;}
.document-module{
  display: flex;
  align-items: center;
  position: relative;
  flex-wrap: wrap;
  color: rgb(38,38,38);
  cursor: pointer;
}
.document-icon{
  width: 18px;
  min-width: 18px;
  height: 18px;
  margin-right: 5px;
  margin-top: 2px;
  text-align: left;
  margin-left: -340px;
  justify-content: center;
  justify-items: center;
  display: inline-block;
  color: inherit;
  font-style: normal;
  line-height: 0;
  text-transform: none;
  text-rendering: optimizeLegibility;
  overflow: hidden;
  white-space: nowrap;
  cursor: pointer;
}
.collect_title{
  color: #585A5A;
  width: 525px;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  box-sizing: border-box;
  cursor: pointer;
  text-align: left;
  position: absolute;
  margin:-18px 0 0 -312px;
  font-size: 14px;
  height: 22px;
}
.documentMenu{
  display: block;
  position: absolute;
  right: 4px;
  top: 0;
  font-size: 14px;
  cursor: default;
  color: #8a8f8d;
  margin: 4px -330px 4px 5px;
  box-sizing: border-box;
  line-height: 22px;
  list-style-position: outside;
  text-align: left;
  white-space: nowrap;
  width: 140px;
  height: 22px;
}
.document-name{
  display: inline-block;
  vertical-align: top;
  font-style: normal;
  margin: -3px 0 -3px 2px;
  position: relative;
  top: 2px;
  color: #8a8f8d;
  border-radius: 4px;
  line-height: 18px;
  box-sizing: border-box;
}
/*跳转*/
.JumpMenu{
  display: block;
  position: absolute;
  right: 4px;
  top: 0;
  font-size: 14px;
  cursor: default;
  color: #8a8f8d;
  width: 58px;
  height: 22px ;
  margin: 0 0 0  5px;
}
/*跳转图标*/
.skipicon{
  display: inline-block;
  vertical-align: top;
  font-style: normal;
  margin: 0 0 0 170px;
  position: relative;
  top: 2px;
  border: 1px solid #d8dad9;
  color: #8a8f8d;
  border-radius: 4px;
  width: 18px;
  height: 18px;
  line-height: 18px;
  box-sizing: border-box;
}
/*页面*/
.page{
  height: 32px;
  line-height: 22px;
  margin: 4px 8px;
  padding: 5px 8px;
  border-radius: 6px;
  overflow: hidden;
  text-overflow: ellipsis;
  cursor: default;
  outline: none !important;
  box-shadow: none !important;
  color: #bec0bf;
  background: none;
  border-color: transparent !important;
  display: block;
  white-space: nowrap;

}
/*上图标*/
.icon-up{
  width: 30px;
  min-width: 30px;
  height: 30px;
  margin-left: 520px;
  margin-top: 15px;
  position: absolute;
  z-index: 1;
}
/*下图标*/
.icon-down{
  width: 30px;
  min-width: 30px;
  height: 30px;
  position: absolute;
  margin-left: 550px;
  margin-top: 15px;
  z-index: 1;
}
/*清空图标*/
.empty{
  position: absolute;
  right: 20px;
  top: 34px;
  align-items: center;
  font-size: 16px;
  text-align: center;
  width: 16px;
  height: 16px;
  z-index: 1;
}
/*搜索线*/
.search_line{
  width: 730px;height: 1px;margin: 18px 0;padding: 0;overflow: hidden;line-height: 0;background-color: rgba(0,0,0,0.06);transform: translateX(-15px);
}
/*页面*/
.data-menu-list{
  font-size: 14px;
  color: #bec0bf;
  line-height: 22px;
  margin-top: 90px;
  margin-left: 10px;
}
/*开始样式*/
.Wrapper{
  height: 32px;line-height: 32px;margin: 4px 8px;padding: 2px 8px;border-radius: 6px;list-style: none;
}
.Wrapper:hover{background-color: #eff0f0;}

/*开始时间*/
.time-on{
  width: 18px;
  min-width: 18px;
  height: 18px;
  margin-right: 5px;
  margin-top: 5px;
  text-align: center;
  justify-content: center;
  justify-items: center;
  display: flex;
}
/*开始内容*/
.start{display:flex;justify-content: center;justify-items: center;   color: #585a5a;width: 525px;display: block;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;line-height: 22px;cursor: pointer;text-align: left;font-size: 14px;margin-top: -19px;margin-left: 30px;}
/*跳转按钮*/
.Jump{
  transform: scaleX(-1) translate(-100px, 0);
  width: 14px;
  min-width: 14px;
  height: 14px;
  text-align: center;
  margin-left: 530px;
  margin-top: -15px;
  position: absolute;
  cursor: initial;
}
/*跳转*/
.Jump_text{font-size: 14px;right: 4px;position: absolute;margin-top: 102px;margin-right: 20px;cursor: default}
/*小记样式*/
.menu-item{height: 32px;line-height: 32px;margin: 4px 8px 0 8px;padding: 2px 8px;border-radius: 6px;list-style: none;}
.menu-item.hovered{background-color: #eff0f0;}
/*百灵图标*/
.lark-icon{
  width: 18px;
  min-width: 18px;
  height: 18px;
  margin-right: 5px;
  margin-top: 5px;
  text-align: center;
  justify-content: center;
  justify-items: center;
  display: flex;
}
/*小记*/
.Notes{display:flex;justify-content: center;justify-items: center;   color: #585a5a;width: 525px;display: block;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;line-height: 22px;cursor: pointer;text-align: left;font-size: 14px;margin-top: -20px;margin-left: 30px;}
/*小记跳转*/
.Jump_abel{font-size: 14px;right: 4px;position: absolute;margin-top: 142px;margin-right: 20px;cursor: default}
/*知识库样式*/
.menu-item-divider{width: 730px;height: 1px;margin: 8px 0;padding: 0;overflow: hidden;line-height: 0;background-color: rgba(0,0,0,0.06);transform: translateX(-10px);}
/*知识库*/
.menu-item-text{height: 24px;line-height: 22px;margin: 0px 3px;padding: 5px 0px;border-radius: 6px;color: #bec0bf;list-style: none;font-size: 14px;}
/*知识库图标*/
.base-icon{width: 18px;min-width: 18px;height: 18px;overflow: hidden;text-align: left;position: absolute;margin-top: 6px}
/*知识库内容*/
.menu-item-default{height: 32px;margin: -4px 8px;padding:2px 8px;border-radius: 6px;color: #bec0bf;list-style: none;font-size: 14px;}
.menu-item-default:hover{background-color: #eff0f0;}
/*默认知识库*/
.base-default{color: rgb(88, 90, 90);width: 525px;overflow: hidden;text-overflow: ellipsis;white-space: nowrap;line-height: 22px;margin-left:30px;text-align: left;height: 22px;position: absolute;margin-top: 235px;}
/*知识库跳转图标*/
.Jump-icon{
  transform: scaleX(-1) translate(-100px, 0);
  width: 14px;
  min-width: 14px;
  height: 14px;
  text-align: center;
  margin-left: 530px;
  margin-top: 8px;
  position: absolute;
  cursor: initial;}
/*知识库跳转*/
.Jump-default{font-size: 14px;right: 4px;position: absolute;margin-top: 230px;margin-right: 20px;cursor: default}
/*盒子方块*/
.square{
  width: 32px; /* 设置盒子的宽度 */
  height: 32px; /* 设置盒子的高度 */
  border: #585A5A 1px solid;
  border-radius: 8px;
  line-height: 32px;
  margin-left: 220px;
  margin-top: -32px;
  display: flex;
  justify-content: center;
  align-items: center;
}
.HeadNewButton{
  position: absolute;
}
/*加号按钮*/
.showbutton{
  width: 33px; /* 设置盒子的宽度 */
  height: 33px; /* 设置盒子的高度 */
  border-radius: 8px;
  margin-left: 220px;
  margin-top: -33px;
  display: flex;
  justify-content: center;
  align-items: center;
}
/*按钮悬停*/
.showbutton:hover{
  background-color: #808080FF;
}
/*加号全局*/

/*下拉菜单*/
.dropdown {
  position: absolute;
  background-color: #fff; /* 默认背景颜色 */
  margin-left: 200px;
  width: 164px;
  height: 300px;
}
/*下拉菜单选项*/
.option {
  padding: 10px;
  cursor: pointer;
  padding-bottom: 10px;
  font-size: 14px;
}
/*悬停选项颜色*/
.option:hover {
  background-color: #f5f5f5; /* 当鼠标悬停时的背景颜色 */
}
/*文档页面*/
.modal {
  background-color: #00fdb9; /* 或者其他你想要的蓝色 */
  width: 520px;
  height: 110px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 24px 24px 24px 24px;
  text-align: left;
  border-radius: 8px;
}
/*关闭页面样式*/
.ant-modal-close-x{
  width: 56px;
  height: 56px;
  line-height: 56px;
  text-align: center;
  cursor: pointer;
  margin-left: 490px;
  margin-top: -25px;
}
/*关闭悬停样式*/
.ant-modal-close-x button{
  cursor: pointer;
}
/*页面标题*/
.module_title{
  position: absolute;
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  margin-right: 100px;
  margin-top: -35px;
  cursor: initial;
}
/*小标题*/
.module_tip{
  color: rgb(138,143,141);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  margin-bottom: 8px;
  cursor: initial;
}
/*内容*/
.book-name{
  align-items: center;
  box-sizing: border-box;
  color: rgb(138, 143, 141);
  display: flex;
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 24px;
  padding: 12px 0px 12px 0px;
  text-align: left;
}
/*下划线*/
.spilt{
  color: rgb(38,38,38);
  font-size: 14px;
  font-weight: 400;
  height: 1px;
  width: 100%;
  list-style: none;
  text-align: left;
  white-space: normal;
  overflow: hidden;
  background-color: rgba(0,0,0,0.06);
}
/*表格页面*/
.from{
  background-color: rgba(222, 213, 47, 0.78); /* 或者其他你想要的蓝色 */
  width: 520px;
  height: 110px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 24px 24px 24px 24px;
  text-align: left;
  border-radius: 8px;
}
/*表格小标题*/
.ftrom_title{
  position: absolute;
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  margin-right: 100px;
  margin-top: -35px;
  cursor: initial;
}
/*画板页面*/
.board{
  background-color: rgba(71, 102, 231, 0.78); /* 或者其他你想要的蓝色 */
  width: 520px;
  height: 110px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 24px 24px 24px 24px;
  text-align: left;
  border-radius: 8px;
}
/*画板小标题*/
.board_title{
  position: absolute;
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  margin-right: 100px;
  margin-top: -35px;
  cursor: initial;
}
/*数据表页面*/
.sheet {
  background-color: rgba(71, 202, 231, 0.78); /* 或者其他你想要的蓝色 */
  width: 520px;
  height: 110px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 24px 24px 24px 24px;
  text-align: left;
  border-radius: 8px;
}
/*数据表小标题*/
.sheet_title{
  position: absolute;
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  margin-right: 100px;
  margin-top: -35px;
  cursor: initial;
}
/*知识库页面头部*/
.base-header{
  left: 40%;
  position: fixed;
  width: 424px;
  height: 42px;
  border-bottom-left-radius: 0;
  border-bottom-right-radius: 0;
  border-top-left-radius: 8px;
  border-top-right-radius: 8px;
  color: rgb(38,38,38);
  border-bottom-color: rgb(38,38,38);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 14px;
  line-height: 22px;
  padding: 20px 24px 0px 24px;
  background-color: blanchedalmond;
}
/*知识库页面标题*/
.base_title{
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 22px;
  list-style-position: outside;
}
/*关闭知识库页面*/
.base-close-x{
  color: rgba(0,0,0,0.75);
  cursor: pointer;
  display: inline-block;
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 700;
  list-style-position: outside;
  text-align: center;
  width: 56px;
  height: 56px;
  line-height: 56px;
  margin-left: 395px;
  position: absolute;
  margin-top: -18px;
}
/*知识库内容样式*/
.base-content{
  background-color: blanchedalmond;
  width: 472px;
  height: 360px;
  position: fixed;
  padding-bottom: 48px;
  left: 40%;
  margin-top: 60px;
}
/*知识库内容*/
.base_tip{
  line-height: 22px;
  font-size: 14px;
  white-space: normal;
  padding: 0 0 8px;
  margin-left: 23px;
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
}
/*空心相册*/
.popover{
  border: 1px solid #d8dad9;
  border-radius: 4px;
  padding: 6px;
  width: 40px;
  height: 40px;
  margin-left: -55px;
  position: absolute;
  line-height: 20px;
  transition: all .3s;
  text-align: center;
  display: inline-block;
  margin-top: 30px;
  background-image: url("../img/知识库.png");
  background-size: cover ;
  background-position: left;
  transform: rotate(-1deg); /* 旋转图片0度，使其不倾斜 */
}
/*知识库输入框*/
.base_input{
  box-sizing: border-box;
  margin-left: 8px;
  display: inline-block;
  position: absolute;
  margin-top: 44px;
  width: 77%;
  min-width: 0;
  padding: 4px 11px;
  line-height: 20px;
  height: 40px;
  border: 1px solid #d8dad9;
  border-radius: 6px;
  transition: all .3s;
}
.base_input:hover{
  border-color: #0BD07D;
  border-right-width: 1px ;
}
.base_input:focus{
  outline: none;
  box-shadow: none;
  border-color: #0BD07D;
}
/*知识库简介*/
.brief{
  height: 98px;
  min-height: 98px;
  max-height: 9007200000000000px;
  resize: none;
  width: 402px;
  padding: 4px 11px 4px 11px;
  border-top-left-radius: 6px;
  border-top-right-radius: 6px;
  border-bottom-left-radius: 6px;
  border-bottom-right-radius: 6px;
  border-right-width: 1px;
  border: 1px solid #d8dad9;
  font-size: 14px;
  margin-left: -55px;
  margin-top: 100px;
  max-width: 100%;
  min-width: 0px;
  position: absolute;
  font-family: -apple-system,blinkmacsystemfont,"Helvetica Neue",helvetica,segoe ui,arial,roboto,"PingFang SC","miui","Hiragino Sans GB","Microsoft Yahei",sans-serif;
}
/*知识库边框颜色*/
.brief:hover{
  border-color: #0BD07D;
  border-right-width: 1px ;
}
/*去掉系统自带的样式*/
.brief:focus{
  outline: none;
  box-shadow: none;
  border-color: #0BD07D;
}
/*新建至*/
.from-item{
  color: rgb(38,38,38);
  font-size: 14px;
  line-height: 22px;
  list-style-position: outside;
  max-width: 100%;
  min-height: 1px;
  padding: 0px 0px 8px 0px;
  width: 376px;
  height: 30px;
  margin-top: 240px;
  margin-left: -55px;
  position: absolute;
  display: inline-block;
  text-align: left;
  float: left;
}
/*头像框*/
.selector{
  height: 40px;
  border:1px solid #d9d9d9 ;
  border-radius: 6px;
  cursor: text;
  padding: 0 11px;
  width: 400px;
  font-size: 14px;
  position: absolute;
  margin-top: 250px;
  margin-left: 25px;
}
.selector:hover{
  border-color: #0bd07D;
  border-right-width: 1px ;
}
/*输入框*/
.select{
  right: 25px;
  position: absolute;
  top: 2px;
  bottom: 0;
  left: 5px;
  height: 30px;
  width: 100%;
  border: none;
  background-color: initial;
  outline: none;
}
/*圆圈*/
.circle{
  width: 24px;
  min-width: 24px;
  height: 24px;
  border-radius: 12px;
  position: absolute;
  border-style: none;
  box-sizing: border-box;
  cursor: pointer;
  line-height: 25px;
}
.menu-light{
  box-shadow: none;
  border-radius: 8px;
  box-sizing: border-box;
  color: #262626;
  font-size: 14px;
  text-align: left;
  width: 360px;
  height: 258px;
  background-color: #fff;
  position: absolute;
  margin-left: -15px;
  margin-top: 10px;
  top: 100%;
  padding: 0 20px 12px 20px;
  z-index: 10;
  border: 1px solid #e7e9e8;
  background-clip: padding-box;
}
.menu-id{
  color: #262626;
  line-height: 40px;
  margin: 4px 6px;
  border-radius: 6px;
  min-height: auto;
  padding: 6px 16px 8px;
  padding-right: 0;
  cursor: text;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  display: block;
  white-space: nowrap;
  box-sizing: border-box;
  width: 278px;
  height: 41.75px;
}
.userInfo{
  display: flex;
  line-height: 40px;
  box-sizing: border-box;
}
.data-click{
 box-sizing: border-box;
}
.img-avatar{
  width: 36px;
  min-width: 36px;
  height: 36px;
  border-radius: 18px;
  border-color: rgba(0, 0, 0, 0.06);
  border-width: 1px;
  border-style: solid;
  box-sizing: border-box;
  vertical-align: middle;
}
.badge-module{
  font-size: 14px;
  line-height: 22px;
  display: flex;
  font-weight: 600;
  box-sizing: border-box;
  width: 188px;
  height: 24.75px;
}
.badge-module_Name{
  line-height: 24px;
  max-width: 450px;
  margin-right: 4px;
  word-break: break-all;
  display: block;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  box-sizing: border-box;
  font-size: 14px;
  text-align: left;
  margin-left: 15px;
  margin-top: 2px;
}
.badge-line{
 position: absolute; width: 278px;height: 1px;margin: 40px 20px;padding: 0;overflow: hidden;line-height: 0;background-color: rgba(0,0,0,0.06);
}
.garden{
  color: #262626;
  height: 40px;
  line-height: 40px;
  margin: 20px 6px;
  border-radius: 6px;
  padding: 0 16px;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  display: block;
  white-space: nowrap;
  cursor: pointer;
  box-sizing: border-box;
  text-align: left;
  font-weight: 400;
  list-style-type:none;
}
.garden:hover{background-color: #eff0f0}
.garden-link{text-decoration: none}
.garden-icon{
  position: relative;
  font-size: 16px;
  color: #8a8f8d;
  top: 1px;
  overflow: hidden;
  display: inline-block;
  line-height: 0;
  text-align: center;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
  box-sizing: border-box;
  width: 16px;
  height: 16px;
}
.text{margin-left: 8px;box-sizing: border-box;font-size: 14px;font-weight: 400;text-decoration: none;color: #262626}
.Creativespace{
  color: #262626;
  height: 40px;
  line-height: 40px;
  margin: -20px 6px;
  border-radius: 6px;
  padding: 0 16px;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  display: block;
  white-space: nowrap;
  cursor: pointer;
  box-sizing: border-box;
  text-align: left;
  list-style: none;
  font-weight: 400;
}
.Creativespace:hover{background-color: #eff0f0}
.creative-link{text-decoration: none}
.creative-icon{
  position: relative;
  font-size: 16px;
  color: #8a8f8d;
  top: 1px;
  overflow: hidden;
  display: inline-block;
  line-height: 0;
  text-align: center;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
  box-sizing: border-box;
  width: 16px;
  height: 16px;}
.space-text{margin-left: 8px;box-sizing: border-box;font-size: 14px;font-weight: 400;text-decoration: none;color: #262626}
.AccountSetting{
  color: #262626;
  height: 40px;
  line-height: 40px;
  margin: 20px 6px;
  border-radius: 6px;
  padding: 0 16px;
  overflow: hidden;
  text-overflow: ellipsis;
  position: relative;
  display: block;
  white-space: nowrap;
  cursor: pointer;
  box-sizing: border-box;
  text-align: left;
  list-style: none;
  font-weight: 400;
}
.AccountSetting:hover{background-color: #eff0f0}
.setting-link{text-decoration: none}
.setting-icon{
  position: relative;
  font-size: 16px;
  color: #8a8f8d;
  top: 1px;
  overflow: hidden;
  display: inline-block;
  line-height: 0;
  text-align: center;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
  box-sizing: border-box;
  width: 16px;
  height: 16px;
}
.setting-text{margin-left: 8px;box-sizing: border-box;font-size: 14px;font-weight: 400;text-decoration: none;color: #262626}
.setting-line{position: absolute; width: 278px;height: 1px;margin: 175px 20px;padding: 0;overflow: hidden;line-height: 0;background-color: rgba(0,0,0,0.06);}
.Logout{width: 195px;border-radius: 6px;padding: 0 15px;cursor: pointer;box-sizing: border-box;line-height: 40px;color: #262626;white-space: nowrap;font-size: 14px;text-align: left;list-style: none;font-weight: 400;}
.Logout:hover{background-color: #eff0f0;}
.logout-icon{
  position: relative;
  font-size: 16px;
  color: #8a8f8d;
  overflow: hidden;
  text-rendering: optimizeLegibility;
  box-sizing: border-box;
  display: inline-block;
  line-height: 0;
  text-align: center;
  vertical-align: -.125em;
  width: 16px;
  height: 16px;
  margin-left: 7px;
}
.Logout-text{margin-left:7px;box-sizing: border-box;cursor: pointer;line-height: 40px;color: #262626;white-space: nowrap;font-size: 14px;text-align: left;font-weight: 400;width: 80px;height: 40px}
.login-out-menu{position:absolute;margin-left:215px;margin-top:-35px;display: flex;align-items: center;box-sizing: border-box;line-height: 40px;cursor: text;color: #262626;white-space: nowrap;font-size: 14px;text-align: left;font-weight: 400;}
.index-module_itemAction{
  height: 32px;
  width: 32px;
  border: 1px solid #e7e9e8;
  border-radius: 6px;
  margin-left: 8px;
  cursor: pointer;
  box-sizing: border-box;
}
.switch{
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
  line-height: 100%;
  color: #8a8f8d;
  overflow: hidden;
  box-sizing: border-box;
}
.switch:hover .tooltip{display: block}
.switch-icon{
  font-size: 20px;
  display: inline-block;
  color: inherit;
  font-style: normal;
  line-height: 0;
  text-align: center;
  text-transform: none;
  vertical-align: -.125em;
  text-rendering: optimizeLegibility;
  box-sizing:border-box;
  width: 20px;
  height: 20px;
}
.tooltip{
  left: 421px;
  top: 222px;
  transform-origin: 50% 40px 0px;
  pointer-events: none;
  width: max-content;
  font-size: 12px;
  padding-bottom: 4px;
  display: none;
  box-sizing: border-box;
  color: #262626;
  line-height: 1.5715;
  list-style: none;
  position: absolute;
  z-index: 1070;
  max-width: 250px;
  visibility: visible;
}
.tooltip-content{
  box-sizing: border-box;
}
.tooltip-arrow{
  left: 50%;
  transform: translateX(-50%);
  bottom: -9.07106781px;
  display: none;
  position: absolute;
  width: 13.07106781px;
  height: 13.07106781px;
  overflow: hidden;
  background: transparent;
  pointer-events: none;
  box-sizing: border-box;
}
.tooltip-arrow-content{
  box-shadow: 3px 3px 7px rgba(0,0,0,.07);
  transform: translateY(-6.53553391px) rotate(45deg);
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: block;
  width: 5px;
  height: 5px;
  margin: auto;
  background-color: rgba(0,0,0,0.75);
  content: "";
  pointer-events: auto;
  box-sizing: border-box;
}
.tooltip-inner{
  min-width: 30px;
  min-height: 32px;
  padding: 6px 8px;
  color: #fff;
  text-align: left;
  text-decoration: none;
  word-wrap: break-word;
  background-color: rgba(0,0,0,0.75);
  border-radius: 6px;
  box-shadow: 0 1px 4px -2px rgba(0,0,0,0.13);
  box-sizing: border-box;
}
/*用户ID*/
.name-title{
  color: #262626;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-left: 40px;
  margin-right: 4px;
  margin-top: -8px;
  width: 70px;
  height: 38px;
  font-size: 14px;
  position: absolute;
}
/*小箭头*/
.arrow-down{
  line-height: 0;
  margin-top: 12px;
  vertical-align: -.125em;
  width: 1em;
  height: 1em;
  float: right;
}
/*复制框*/
.repeated-element-bg{
  margin-left: -14px;
  width: 424px;
  min-width: 24px;
  height: 42px;
  position: absolute;
  top: -55px;
  background-color: #e1dede;
  box-shadow: 0 8px 16px 4px rgba(0,0,0,.04);
  border: 1px solid #e7e9e8;
  border-radius: 8px;
}
/*复制头像*/
.Avatar-clone{
  width: 24px;
  min-width: 24px;
  height: 24px;
  border-radius: 12px;
  position: absolute;
  top: 8px;
  margin-left: 12px;
}
/*复制用户ID*/
.name-clone{
  color: #262626;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-left: 52px;
  margin-right: 4px;
  margin-top: -8px;
  width: 70px;
  height: 38px;
  font-size: 14px;
  position: absolute;
}
/*新建按钮*/
.submitbtn{
  height: 42px;
  width: 424px;
  padding: 4px 15px 4px 15px;
  background-color: rgb(0, 185, 107);
  border-radius: 6px;
  border: none;
  border-bottom-width: 0;
  margin-top: 320px;
  margin-left: 25px;
  position: absolute;
}
.submitbtn:hover{
  background-color: #009456;
}



/*导入页面*/
.import {
  background-color: rgb(188, 133, 227); /* 或者其他你想要的蓝色 */
  width: 520px;
  height: 110px;
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 24px 24px 24px 24px;
  text-align: left;
  border-radius: 8px;
}
/*导入小标题*/
.import_title{
  position: absolute;
  color: rgba(0,0,0,0.85);
  font-family: Chinese Quote, -apple-system, BlinkMacSystemFont, Segoe UI, Roboto, PingFang SC, Hiragino Sans GB, Microsoft YaHei, Helvetica Neue, Helvetica, Arial, sans-serif;
  font-size: 16px;
  font-weight: 500;
  line-height: 24px;
  margin-right: 100px;
  margin-top: -35px;
  cursor: initial;
}
</style>
