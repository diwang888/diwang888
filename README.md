<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CY俱乐部 - 专业护航服务</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: "PingFang SC", sans-serif;
        }
        body {
            background: #f5f5f5;
            color: #333;
        }
        
        /* 登录界面样式 */
        .login-container {
            max-width: 400px;
            margin: 100px auto;
            padding: 20px;
            background: white;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0,0,0,0.1);
        }
        .login-container h2 {
            text-align: center;
            margin-bottom: 20px;
            color: #f0a22e;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
            font-weight: bold;
        }
        .form-group input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
        }
        .login-btn {
            width: 100%;
            padding: 10px;
            background: #f0a22e;
            color: white;
            border: none;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
        }
        .login-btn:hover {
            background: #e67e22;
        }
        .login-error {
            color: red;
            text-align: center;
            margin-top: 10px;
            display: none;
        }
        
        /* 主界面样式 */
        #main-content {
            display: none;
        }
        header {
            background: linear-gradient(135deg, #f0a22e, #e67e22);
            color: white;
            padding: 15px;
            text-align: center;
            font-weight: bold;
            position: fixed;
            width: 100%;
            top: 0;
            z-index: 100;
        }
        main {
            margin-top: 60px;
            padding: 15px;
            margin-bottom: 70px;
        }
        .product-card {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
            transition: transform 0.3s;
        }
        .product-card:active {
            transform: scale(0.98);
        }
        .product-title {
            font-size: 16px;
            font-weight: bold;
            margin-bottom: 8px;
            color: #f0a22e;
        }
        .product-desc {
            font-size: 14px;
            color: #666;
            margin-bottom: 12px;
        }
        .product-footer {
            display: flex;
            justify-content: space-between;
            align-items: center;
        }
        .product-price {
            color: #ff5722;
            font-weight: bold;
            font-size: 16px;
        }
        .buy-btn {
            background: #f0a22e;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            font-size: 14px;
            cursor: pointer;
        }
        .buy-btn:active {
            background: #d68910;
        }
        .buy-btn.disabled {
            background: #ccc;
            cursor: not-allowed;
        }
        .bottom-nav {
            position: fixed;
            bottom: 0;
            width: 100%;
            background: white;
            display: flex;
            justify-content: space-around;
            padding: 12px 0;
            box-shadow: 0 -2px 5px rgba(0,0,0,0.1);
        }
        .nav-item {
            display: flex;
            flex-direction: column;
            align-items: center;
            font-size: 12px;
            color: #666;
            cursor: pointer;
        }
        .nav-item.active {
            color: #f0a22e;
        }
        
        /* 订单页面样式 */
        .order-list, .forum-page, .admin-page {
            display: none;
        }
        .order-item, .forum-post {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .order-title, .post-author {
            font-weight: bold;
            margin-bottom: 5px;
        }
        .order-time, .post-time {
            font-size: 12px;
            color: #999;
        }
        .post-content {
            margin-top: 10px;
        }
        
        /* 论坛发帖区 */
        .post-form {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .post-input {
            width: 100%;
            padding: 10px;
            border: 1px solid #ddd;
            border-radius: 5px;
            margin-bottom: 10px;
            resize: none;
        }
        .submit-post {
            background: #f0a22e;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
        }
        
        /* 管理员页面 */
        .admin-section {
            background: white;
            border-radius: 8px;
            padding: 15px;
            margin-bottom: 15px;
            box-shadow: 0 2px 5px rgba(0,0,0,0.1);
        }
        .admin-title {
            font-weight: bold;
            margin-bottom: 10px;
            color: #f0a22e;
        }
        .admin-btn {
            background: #3498db;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            margin-right: 10px;
            margin-bottom: 10px;
        }
        .user-list {
            margin-top: 10px;
        }
        .user-item {
            display: flex;
            justify-content: space-between;
            padding: 8px 0;
            border-bottom: 1px solid #eee;
        }
        .ban-btn {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 3px 8px;
            border-radius: 3px;
            cursor: pointer;
        }
        
        /* 模态框样式 */
        .modal {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: rgba(0,0,0,0.5);
            z-index: 1000;
            justify-content: center;
            align-items: center;
        }
        .modal-content {
            background: white;
            padding: 20px;
            border-radius: 10px;
            width: 90%;
            max-width: 400px;
            max-height: 80vh;
            overflow-y: auto;
        }
        .modal-title {
            font-size: 18px;
            margin-bottom: 15px;
            color: #f0a22e;
            text-align: center;
        }
        .close-btn {
            float: right;
            cursor: pointer;
        }
        .form-group {
            margin-bottom: 15px;
        }
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        .form-group input, .form-group textarea, .form-group select {
            width: 100%;
            padding: 8px;
            border: 1px solid #ddd;
            border-radius: 4px;
        }
        .save-btn {
            background: #2ecc71;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }
        .cancel-btn {
            background: #e74c3c;
            color: white;
            border: none;
            padding: 8px 15px;
            border-radius: 4px;
            cursor: pointer;
            margin-top: 10px;
            width: 100%;
        }
        
        /* 购买成功弹窗 */
        .purchase-modal {
            text-align: center;
        }
        .info-text {
            margin: 10px 0;
            color: #666;
        }
        .important-note {
            color: #e74c3c;
            font-weight: bold;
            margin-top: 15px;
        }
        
        /* 订单详情样式 */
        .order-detail {
            margin-bottom: 10px;
            padding: 10px;
            background: #f9f9f9;
            border-radius: 5px;
        }
        .detail-label {
            font-weight: bold;
            color: #666;
        }
        .detail-value {
            margin-left: 10px;
        }
    </style>
</head>
<body>
    <!-- 登录界面 -->
    <div id="login-container" class="login-container">
        <h2>CY俱乐部</h2>
        <div class="form-group">
            <label for="username">账号</label>
            <input type="text" id="username" placeholder="请输入账号">
        </div>
        <div class="form-group">
            <label for="password">密码</label>
            <input type="password" id="password" placeholder="请输入密码">
        </div>
        <button id="login-btn" class="login-btn">登录</button>
        <div id="login-error" class="login-error">账号或密码错误，或账号已被封禁</div>
    </div>
    
    <!-- 主界面 -->
    <div id="main-content">
        <header>
            CY俱乐部专业护航
            <span id="user-info" style="font-size:12px;float:right;"></span>
        </header>

        <!-- 首页 -->
        <main id="home-page">
            <div id="products-container">
                <!-- 商品将通过JS动态加载 -->
            </div>
        </main>

        <!-- 订单页面 -->
        <main id="order-page" class="order-list">
            <h3 style="text-align:center;margin-bottom:15px;">我的订单</h3>
            <div id="orders-container"></div>
        </main>

        <!-- 论坛页面 -->
        <main id="forum-page" class="forum-page">
            <h3 style="text-align:center;margin-bottom:15px;">俱乐部论坛</h3>
            <div class="post-form">
                <textarea id="post-content" class="post-input" placeholder="发表你的想法..."></textarea>
                <button id="submit-post" class="submit-post">发布</button>
            </div>
            <div id="posts-container"></div>
        </main>

        <!-- 管理员页面 -->
        <main id="admin-page" class="admin-page">
            <h3 style="text-align:center;margin-bottom:15px;">管理员面板</h3>
            
            <div class="admin-section">
                <div class="admin-title">客户订单</div>
                <div id="admin-orders-container"></div>
            </div>
            
            <div class="admin-section">
                <div class="admin-title">商品管理</div>
                <button class="admin-btn" onclick="showAddProductModal()">新增商品</button>
                <button class="admin-btn" onclick="showEditProductModal()">编辑商品</button>
                <button class="admin-btn" onclick="showDeleteProductModal()">删除商品</button>
                <div id="products-management-list"></div>
            </div>
            
            <div class="admin-section">
                <div class="admin-title">账号管理</div>
                <div class="user-list" id="user-management-list">
                    <!-- 用户列表将通过JS动态加载 -->
                </div>
            </div>
        </main>

        <div class="bottom-nav">
            <div class="nav-item active" onclick="showPage('home-page')">
                <span>🏠</span>
                <span>首页</span>
            </div>
            <div class="nav-item" onclick="showPage('order-page')">
                <span>🛒</span>
                <span>订单</span>
            </div>
            <div class="nav-item" onclick="showPage('forum-page')">
                <span>💬</span>
                <span>论坛</span>
            </div>
            <div class="nav-item" onclick="showPage('admin-page')">
                <span>👑</span>
                <span>我的</span>
            </div>
        </div>
    </div>
    
    <!-- 填写订单信息模态框 -->
    <div id="order-info-modal" class="modal">
        <div class="modal-content">
            <h3 class="modal-title">填写订单信息</h3>
            <div class="form-group">
                <label>选择区服</label>
                <select id="game-server" class="form-group input">
                    <option value="QQ区">QQ区</option>
                    <option value="微信区">微信区</option>
                </select>
            </div>
            <div class="form-group">
                <label>游戏名称</label>
                <input type="text" id="game-name" placeholder="请输入游戏名称">
            </div>
            <div class="form-group">
                <label>游戏ID</label>
                <input type="text" id="game-id" placeholder="请输入游戏ID">
            </div>
            <div class="form-group">
                <label>你的QQ号</label>
                <input type="text" id="customer-qq" placeholder="请输入你的QQ号">
            </div>
            <div class="form-group">
                <label>订单备注</label>
                <textarea id="order-note" placeholder="请输入订单备注信息"></textarea>
            </div>
            <button class="save-btn" onclick="submitOrderInfo()">确认提交</button>
            <button class="cancel-btn" onclick="closeModal()">取消</button>
        </div>
    </div>
    
    <!-- 购买成功模态框 -->
    <div id="purchase-modal" class="modal">
        <div class="modal-content purchase-modal">
            <h3 class="modal-title">订单提交成功！</h3>
            <div class="order-detail">
                <div><span class="detail-label">商品名称:</span> <span class="detail-value" id="success-product-name"></span></div>
                <div><span class="detail-label">价格:</span> <span class="detail-value" id="success-product-price"></span></div>
                <div><span class="detail-label">区服:</span> <span class="detail-value" id="success-server"></span></div>
                <div><span class="detail-label">游戏名称:</span> <span class="detail-value" id="success-game-name"></span></div>
                <div><span class="detail-label">游戏ID:</span> <span class="detail-value" id="success-game-id"></span></div>
                <div><span class="detail-label">你的QQ号:</span> <span class="detail-value" id="success-customer-qq"></span></div>
                <div><span class="detail-label">订单备注:</span> <span class="detail-value" id="success-order-note"></span></div>
            </div>
            <p class="info-text">请耐心等待客服联系你</p>
            <p class="important-note">注意：请确保游戏和QQ的好友添加功能已开启</p>
            <button class="save-btn" onclick="closeModal()">确定</button>
        </div>
    </div>
    
    <!-- 新增商品模态框 -->
    <div id="add-product-modal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">×</span>
            <h3 class="modal-title">新增商品</h3>
            <div class="form-group">
                <label>商品名称</label>
                <input type="text" id="new-product-name" placeholder="输入商品名称">
            </div>
            <div class="form-group">
                <label>商品描述</label>
                <textarea id="new-product-desc" placeholder="输入商品描述"></textarea>
            </div>
            <div class="form-group">
                <label>商品价格</label>
                <input type="number" id="new-product-price" placeholder="输入价格">
            </div>
            <div class="form-group">
                <label>每日限购次数</label>
                <input type="number" id="new-product-limit" placeholder="输入限购次数（0为不限购）" value="0">
            </div>
            <button class="save-btn" onclick="addProduct()">保存</button>
        </div>
    </div>
    
    <!-- 编辑商品模态框 -->
    <div id="edit-product-modal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">×</span>
            <h3 class="modal-title">编辑商品</h3>
            <div class="form-group">
                <label>选择商品</label>
                <select id="edit-product-select" class="form-group input" onchange="loadProductData()">
                    <!-- 选项将通过JS动态加载 -->
                </select>
            </div>
            <div class="form-group">
                <label>商品名称</label>
                <input type="text" id="edit-product-name" placeholder="输入商品名称">
            </div>
            <div class="form-group">
                <label>商品描述</label>
                <textarea id="edit-product-desc" placeholder="输入商品描述"></textarea>
            </div>
            <div class="form-group">
                <label>商品价格</label>
                <input type="number" id="edit-product-price" placeholder="输入价格">
            </div>
            <div class="form-group">
                <label>每日限购次数</label>
                <input type="number" id="edit-product-limit" placeholder="输入限购次数（0为不限购）">
            </div>
            <button class="save-btn" onclick="saveProductChanges()">保存</button>
        </div>
    </div>
    
    <!-- 删除商品模态框 -->
    <div id="delete-product-modal" class="modal">
        <div class="modal-content">
            <span class="close-btn" onclick="closeModal()">×</span>
            <h3 class="modal-title">删除商品</h3>
            <div class="form-group">
                <label>选择要删除的商品</label>
                <select id="delete-product-select" class="form-group input">
                    <!-- 选项将通过JS动态加载 -->
                </select>
            </div>
            <button class="save-btn" style="background:#e74c3c;" onclick="deleteProduct()">确认删除</button>
        </div>
    </div>
    
    <script>
        // 当前登录用户
        let currentUser = null;
        // 订单数据
        let orders = [];
        // 论坛帖子数据
        let forumPosts = [];
        // 用户数据
        let allUsers = [];
        // 黑名单
        let blacklist = [];
        // 商品数据
        let products = [
            {
                id: 1,
                name: "福利单保底300w",
                desc: "老板点图（除一图和苏尔南）",
                price: 3,
                dailyLimit: 1
            },
            {
                id: 2,
                name: "特惠单保底500w",
                desc: "老板点图（除一图和苏尔南）",
                price: 6,
                dailyLimit: 0
            },
            {
                id: 3,
                name: "赌鸡单",
                desc: "老板点图（除一图和苏尔南）",
                price: 7.5,
                dailyLimit: 0
            }
        ];
        // 用户购买记录
        let userPurchases = {};
        // 管理员订单数据
        let adminOrders = [];
        
        // 预定义账号
        const predefinedAccounts = [
            { username: "diwang", password: "888888", role: "superadmin" },
            { username: "111", password: "111111", role: "admin" },
            { username: "222", password: "222222", role: "admin" }
        ];
        
        // 初始化数据
        function initData() {
            // 从本地存储加载数据
            if(localStorage.getItem("cy_club_products")) {
                products = JSON.parse(localStorage.getItem("cy_club_products"));
            }
            
            if(localStorage.getItem("cy_club_users")) {
                allUsers = JSON.parse(localStorage.getItem("cy_club_users"));
            } else {
                allUsers = predefinedAccounts;
                saveUsers();
            }
            
            if(localStorage.getItem("cy_club_blacklist")) {
                blacklist = JSON.parse(localStorage.getItem("cy_club_blacklist"));
            }
            
            if(localStorage.getItem("cy_club_posts")) {
                forumPosts = JSON.parse(localStorage.getItem("cy_club_posts"));
            }
            
            if(localStorage.getItem("cy_club_purchases")) {
                userPurchases = JSON.parse(localStorage.getItem("cy_club_purchases"));
            }
            
            if(localStorage.getItem("cy_club_admin_orders")) {
                adminOrders = JSON.parse(localStorage.getItem("cy_club_admin_orders"));
            }
            
            // 加载当前用户订单
            if(currentUser && localStorage.getItem(`cy_club_orders_${currentUser.username}`)) {
                orders = JSON.parse(localStorage.getItem(`cy_club_orders_${currentUser.username}`));
            }
        }
        
        // 保存数据到本地存储
        function saveProducts() {
            localStorage.setItem("cy_club_products", JSON.stringify(products));
        }
        
        function saveUsers() {
            localStorage.setItem("cy_club_users", JSON.stringify(allUsers));
        }
        
        function saveBlacklist() {
            localStorage.setItem("cy_club_blacklist", JSON.stringify(blacklist));
        }
        
        function savePosts() {
            localStorage.setItem("cy_club_posts", JSON.stringify(forumPosts));
        }
        
        function savePurchases() {
            localStorage.setItem("cy_club_purchases", JSON.stringify(userPurchases));
        }
        
        function saveAdminOrders() {
            localStorage.setItem("cy_club_admin_orders", JSON.stringify(adminOrders));
        }
        
        function saveOrders() {
            if(currentUser) {
                localStorage.setItem(`cy_club_orders_${currentUser.username}`, JSON.stringify(orders));
            }
        }
        
        // 登录功能
        document.getElementById('login-btn').addEventListener('click', function() {
            const username = document.getElementById('username').value;
            const password = document.getElementById('password').value;
            const errorElement = document.getElementById('login-error');
            
            // 检查黑名单
            if(blacklist.includes(username)) {
                errorElement.textContent = "该账号已被封禁，无法登录";
                errorElement.style.display = "block";
                return;
            }
            
            // 检查预定义账号
            const predefinedAccount = predefinedAccounts.find(acc => 
                acc.username === username && acc.password === password
            );
            
            if(predefinedAccount) {
                // 预定义账号登录
                currentUser = {
                    username: predefinedAccount.username,
                    role: predefinedAccount.role
                };
                successfulLogin();
                return;
            }
            
            // 检查已注册用户
            const existingUser = allUsers.find(user => 
                user.username === username && user.password === password
            );
            
            if(existingUser) {
                currentUser = {
                    username: existingUser.username,
                    role: "user"
                };
                successfulLogin();
                return;
            }
            
            // 新用户自动注册
            if(username && password) {
                allUsers.push({
                    username,
                    password,
                    role: "user"
                });
                saveUsers();
                
                currentUser = {
                    username,
                    role: "user"
                };
                successfulLogin();
                return;
            }
            
            // 登录失败
            errorElement.style.display = "block";
        });
        
        function successfulLogin() {
            document.getElementById('login-container').style.display = 'none';
            document.getElementById('main-content').style.display = 'block';
            
            // 显示用户信息
            const userInfoElement = document.getElementById('user-info');
            userInfoElement.textContent = currentUser.username;
            if(currentUser.role === "superadmin") {
                userInfoElement.textContent += " (超级管理员)";
            } else if(currentUser.role === "admin") {
                userInfoElement.textContent += " (管理员)";
            }
            
            // 初始化数据
            initData();
            
            // 加载内容
            renderProducts();
            renderOrders();
            renderForumPosts();
            renderUserList();
            renderAdminOrders();
            
            // 如果是普通用户，隐藏管理员页面
            if(currentUser.role === "user") {
                document.querySelector('.bottom-nav .nav-item:nth-child(4)').style.display = 'none';
            } else {
                document.querySelector('.bottom-nav .nav-item:nth-child(4)').style.display = 'flex';
            }
        }
        
        // 页面切换
        function showPage(pageId) {
            // 隐藏所有页面
            document.getElementById('home-page').style.display = 'none';
            document.getElementById('order-page').style.display = 'none';
            document.getElementById('forum-page').style.display = 'none';
            document.getElementById('admin-page').style.display = 'none';
            
            // 显示目标页面
            document.getElementById(pageId).style.display = 'block';
            
            // 更新底部导航状态
            const navItems = document.querySelectorAll('.nav-item');
            navItems.forEach(item => {
                item.classList.remove('active');
            });
            event.currentTarget.classList.add('active');
            
            // 如果是论坛页面，滚动到底部
            if(pageId === 'forum-page') {
                setTimeout(() => {
                    window.scrollTo(0, document.body.scrollHeight);
                }, 100);
            }
            
            // 如果是管理员页面且是超级管理员，刷新订单列表
            if(pageId === 'admin-page' && currentUser.role === "superadmin") {
                renderAdminOrders();
            }
        }
        
        // 商品相关功能
        function renderProducts() {
            const container = document.getElementById('products-container');
            container.innerHTML = '';
            
            const today = new Date().toDateString();
            
            products.forEach(product => {
                const productCard = document.createElement('div');
                productCard.className = 'product-card';
                
                // 检查用户今日是否已购买过限购商品
                let canPurchase = true;
                if(product.dailyLimit > 0 && currentUser) {
                    const userPurchaseKey = `${currentUser.username}_${product.id}_${today}`;
                    const purchaseCount = userPurchases[userPurchaseKey] || 0;
                    if(purchaseCount >= product.dailyLimit) {
                        canPurchase = false;
                    }
                }
                
                productCard.innerHTML = `
                    <div class="product-title">${product.name}</div>
                    <div class="product-desc">${product.desc}</div>
                    <div class="product-footer">
                        <div class="product-price">¥${product.price.toFixed(2)}</div>
                        <button class="buy-btn ${!canPurchase ? 'disabled' : ''}" 
                                onclick="${canPurchase ? `showOrderInfoModal(${product.id})` : ''}">
                            ${canPurchase ? '立即购买' : '今日已购'}
                        </button>
                    </div>
                `;
                
                container.appendChild(productCard);
            });
        }
        
        function showOrderInfoModal(productId) {
            document.getElementById('order-info-modal').style.display = 'flex';
            document.getElementById('order-info-modal').setAttribute('data-product-id', productId);
            
            // 清空表单
            document.getElementById('game-server').value = 'QQ区';
            document.getElementById('game-name').value = '';
            document.getElementById('game-id').value = '';
            document.getElementById('customer-qq').value = '';
            document.getElementById('order-note').value = '';
        }
        
        function submitOrderInfo() {
            const productId = parseInt(document.getElementById('order-info-modal').getAttribute('data-product-id'));
            const product = products.find(p => p.id === productId);
            if(!product) return;
            
            const server = document.getElementById('game-server').value;
            const gameName = document.getElementById('game-name').value.trim();
            const gameId = document.getElementById('game-id').value.trim();
            const customerQQ = document.getElementById('customer-qq').value.trim();
            const orderNote = document.getElementById('order-note').value.trim();
            
            if(!gameName || !gameId || !customerQQ) {
                alert('请填写完整的游戏信息');
                return;
            }
            
            // 记录订单
            const order = {
                productId: product.id,
                productName: product.name,
                price: product.price,
                time: new Date().toLocaleString(),
                server,
                gameName,
                gameId,
                customerQQ,
                orderNote,
                customer: currentUser.username
            };
            
            orders.unshift(order);
            saveOrders();
            
            // 添加到管理员订单列表
            adminOrders.unshift(order);
            saveAdminOrders();
            
            // 记录购买次数（用于限购）
            const today = new Date().toDateString();
            const userPurchaseKey = `${currentUser.username}_${product.id}_${today}`;
            userPurchases[userPurchaseKey] = (userPurchases[userPurchaseKey] || 0) + 1;
            savePurchases();
            
            // 显示购买成功信息
            document.getElementById('success-product-name').textContent = product.name;
            document.getElementById('success-product-price').textContent = `¥${product.price.toFixed(2)}`;
            document.getElementById('success-server').textContent = server;
            document.getElementById('success-game-name').textContent = gameName;
            document.getElementById('success-game-id').textContent = gameId;
            document.getElementById('success-customer-qq').textContent = customerQQ;
            document.getElementById('success-order-note').textContent = orderNote || '无';
            
            // 关闭填写表单，显示成功信息
            closeModal();
            document.getElementById('purchase-modal').style.display = 'flex';
            
            // 更新订单列表
            renderOrders();
            // 刷新商品列表（更新购买按钮状态）
            renderProducts();
        }
        
        // 订单相关功能
        function renderOrders() {
            const container = document.getElementById('orders-container');
            container.innerHTML = '';
            
            if(orders.length === 0) {
                container.innerHTML = '<p style="text-align:center;color:#999;">暂无订单记录</p>';
                return;
            }
            
            orders.forEach(order => {
                const orderItem = document.createElement('div');
                orderItem.className = 'order-item';
                orderItem.innerHTML = `
                    <div class="order-title">${order.productName}</div>
                    <div>价格: ¥${order.price.toFixed(2)}</div>
                    <div>区服: ${order.server}</div>
                    <div>游戏ID: ${order.gameId}</div>
                    <div class="order-time">${order.time}</div>
                    <div>状态: 等待处理</div>
                `;
                container.appendChild(orderItem);
            });
        }
        
        // 管理员订单列表
        function renderAdminOrders() {
            if(currentUser.role !== "superadmin") return;
            
            const container = document.getElementById('admin-orders-container');
            container.innerHTML = '';
            
            if(adminOrders.length === 0) {
                container.innerHTML = '<p style="text-align:center;color:#999;">暂无客户订单</p>';
                return;
            }
            
            // 按时间倒序排列
            const sortedOrders = [...adminOrders].sort((a, b) => new Date(b.time) - new Date(a.time));
            
            sortedOrders.forEach(order => {
                const orderItem = document.createElement('div');
                orderItem.className = 'order-item';
                orderItem.innerHTML = `
                    <div class="order-title">${order.productName} - ${order.customer}</div>
                    <div class="order-detail">
                        <div><span class="detail-label">价格:</span> <span class="detail-value">¥${order.price.toFixed(2)}</span></div>
                        <div><span class="detail-label">区服:</span> <span class="detail-value">${order.server}</span></div>
                        <div><span class="detail-label">游戏名称:</span> <span class="detail-value">${order.gameName}</span></div>
                        <div><span class="detail-label">游戏ID:</span> <span class="detail-value">${order.gameId}</span></div>
                        <div><span class="detail-label">客户QQ:</span> <span class="detail-value">${order.customerQQ}</span></div>
                        <div><span class="detail-label">订单备注:</span> <span class="detail-value">${order.orderNote || '无'}</span></div>
                    </div>
                    <div class="order-time">${order.time}</div>
                `;
                container.appendChild(orderItem);
            });
        }
        
        // 论坛相关功能
        function renderForumPosts() {
            const container = document.getElementById('posts-container');
            container.innerHTML = '';
            
            if(forumPosts.length === 0) {
                container.innerHTML = '<p style="text-align:center;color:#999;">暂无帖子</p>';
                return;
            }
            
            // 按时间倒序排列
            const sortedPosts = [...forumPosts].sort((a, b) => new Date(b.time) - new Date(a.time));
            
            sortedPosts.forEach(post => {
                const postElement = document.createElement('div');
                postElement.className = 'forum-post';
                postElement.innerHTML = `
                    <div class="post-author">${post.author}</div>
                    <div class="post-time">${new Date(post.time).toLocaleString()}</div>
                    <div class="post-content">${post.content}</div>
                `;
                container.appendChild(postElement);
            });
        }
        
        document.getElementById('submit-post').addEventListener('click', function() {
            const content = document.getElementById('post-content').value.trim();
            if(!content) return;
            
            const newPost = {
                author: currentUser.username,
                content: content,
                time: new Date().toISOString()
            };
            
            forumPosts.push(newPost);
            savePosts();
            
            // 清空输入框
            document.getElementById('post-content').value = '';
            
            // 刷新帖子列表
            renderForumPosts();
            
            // 滚动到底部查看新帖子
            setTimeout(() => {
                window.scrollTo(0, document.body.scrollHeight);
            }, 100);
        });
        
        // 管理员功能
        function renderUserList() {
            if(currentUser.role !== "superadmin") return;
            
            const container = document.getElementById('user-management-list');
            container.innerHTML = '';
            
            // 按用户名排序
            const sortedUsers = [...allUsers].sort((a, b) => a.username.localeCompare(b.username));
            
            sortedUsers.forEach(user => {
                if(user.role === "superadmin") return; // 不显示超级管理员自己
                
                const userItem = document.createElement('div');
                userItem.className = 'user-item';
                
                const isBanned = blacklist.includes(user.username);
                
                userItem.innerHTML = `
                    <span style="${isBanned ? 'text-decoration:line-through;color:#999;' : ''}">
                        ${user.username} (${user.role === "admin" ? "管理员" : "用户"})
                    </span>
                    <button class="ban-btn" onclick="toggleBanUser('${user.username}')">
                        ${isBanned ? '解封' : '封禁'}
                    </button>
                `;
                
                container.appendChild(userItem);
            });
        }
        
        function toggleBanUser(username) {
            const index = blacklist.indexOf(username);
            if(index === -1) {
                blacklist.push(username);
            } else {
                blacklist.splice(index, 1);
            }
            saveBlacklist();
            renderUserList();
        }
        
        // 商品管理功能
        function showAddProductModal() {
            document.getElementById('add-product-modal').style.display = 'flex';
        }
        
        function showEditProductModal() {
            const selectElement = document.getElementById('edit-product-select');
            selectElement.innerHTML = '';
            
            products.forEach(product => {
                const option = document.createElement('option');
                option.value = product.id;
                option.textContent = product.name;
                selectElement.appendChild(option);
            });
            
            if(products.length > 0) {
                loadProductData();
            }
            
            document.getElementById('edit-product-modal').style.display = 'flex';
        }
        
        function showDeleteProductModal() {
            const selectElement = document.getElementById('delete-product-select');
            selectElement.innerHTML = '';
            
            products.forEach(product => {
                const option = document.createElement('option');
                option.value = product.id;
                option.textContent = product.name;
                selectElement.appendChild(option);
            });
            
            document.getElementById('delete-product-modal').style.display = 'flex';
        }
        
        function loadProductData() {
            const productId = parseInt(document.getElementById('edit-product-select').value);
            const product = products.find(p => p.id === productId);
            
            if(product) {
                document.getElementById('edit-product-name').value = product.name;
                document.getElementById('edit-product-desc').value = product.desc;
                document.getElementById('edit-product-price').value = product.price;
                document.getElementById('edit-product-limit').value = product.dailyLimit;
            }
        }
        
        function addProduct() {
            const name = document.getElementById('new-product-name').value.trim();
            const desc = document.getElementById('new-product-desc').value.trim();
            const price = parseFloat(document.getElementById('new-product-price').value);
            const limit = parseInt(document.getElementById('new-product-limit').value) || 0;
            
            if(!name || !desc || isNaN(price)) {
                alert('请填写完整信息');
                return;
            }
            
            const newId = products.length > 0 ? Math.max(...products.map(p => p.id)) + 1 : 1;
            
            products.push({
                id: newId,
                name: name,
                desc: desc,
                price: price,
                dailyLimit: limit
            });
            
            saveProducts();
            closeModal();
            renderProducts();
            
            // 清空表单
            document.getElementById('new-product-name').value = '';
            document.getElementById('new-product-desc').value = '';
            document.getElementById('new-product-price').value = '';
            document.getElementById('new-product-limit').value = '0';
        }
        
        function saveProductChanges() {
            const productId = parseInt(document.getElementById('edit-product-select').value);
            const name = document.getElementById('edit-product-name').value.trim();
            const desc = document.getElementById('edit-product-desc').value.trim();
            const price = parseFloat(document.getElementById('edit-product-price').value);
            const limit = parseInt(document.getElementById('edit-product-limit').value) || 0;
            
            if(!name || !desc || isNaN(price)) {
                alert('请填写完整信息');
                return;
            }
            
            const productIndex = products.findIndex(p => p.id === productId);
            if(productIndex !== -1) {
                products[productIndex] = {
                    ...products[productIndex],
                    name: name,
                    desc: desc,
                    price: price,
                    dailyLimit: limit
                };
                
                saveProducts();
                closeModal();
                renderProducts();
            }
        }
        
        function deleteProduct() {
            const productId = parseInt(document.getElementById('delete-product-select').value);
            const productIndex = products.findIndex(p => p.id === productId);
            
            if(productIndex !== -1) {
                if(confirm(`确定要删除 "${products[productIndex].name}" 吗？`)) {
                    products.splice(productIndex, 1);
                    saveProducts();
                    closeModal();
                    renderProducts();
                }
            }
        }
        
        // 通用功能
        function closeModal() {
            document.querySelectorAll('.modal').forEach(modal => {
                modal.style.display = 'none';
            });
        }
        
        // 初始化
        initData();
        
        // 监听键盘事件（论坛发帖按Enter+Ctrl提交）
        document.getElementById('post-content').addEventListener('keydown', function(e) {
            if(e.key === 'Enter' && e.ctrlKey) {
                document.getElementById('submit-post').click();
            }
        });
    </script>
</body>
</html>
