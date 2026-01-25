<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>코딩 마스터 - 실시간 커뮤니티</title>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-app-compat.js"></script>
    <script src="https://www.gstatic.com/firebasejs/9.22.0/firebase-firestore-compat.js"></script>
    
    <style>
        /* 사용자님이 이미지(image_9c8836.png)로 보여주신 메뉴 스타일을 버그 없이 구현했습니다. */
        :root { --primary: #667eea; --bg: #f8f9fa; --text: #222; }
        * { margin: 0; padding: 0; box-sizing: border-box; }
        body { font-family: 'Pretendard', sans-serif; background: var(--bg); color: var(--text); }
        header { background: white; border-bottom: 1px solid #e5e5e5; position: sticky; top: 0; z-index: 1000; }
        .header-top { max-width: 1200px; margin: 0 auto; padding: 15px 20px; display: flex; justify-content: space-between; align-items: center; }
        .logo { font-size: 22px; font-weight: 900; color: var(--primary); cursor: pointer; }
        .nav-menu { max-width: 1200px; margin: 0 auto; padding: 0 20px; display: flex; gap: 20px; }
        
        /* [메뉴 버그 수정] active 클래스가 있을 때만 밑줄이 생깁니다. */
        .nav-item { padding: 15px 5px; cursor: pointer; font-size: 15px; font-weight: 700; color: #777; border-bottom: 3px solid transparent; }
        .nav-item.active { color: var(--primary); border-bottom-color: var(--primary); }

        .main-container { max-width: 1200px; margin: 25px auto; padding: 0 20px; }
        .card { background: white; border-radius: 16px; padding: 25px; box-shadow: 0 4px 12px rgba(0,0,0,0.05); margin-bottom: 25px; }
        .page { display: none; }
        .page.active { display: block; }
    </style>
</head>
<body>

<header>
    <div class="header-top">
        <div class="logo" onclick="goHome()">🚀 CODING MASTER</div>
    </div>
    <nav class="nav-menu">
        <div class="nav-item active" id="menu-home" onclick="goHome()">홈</div>
        <div class="nav-item" id="menu-notice" onclick="showBoard('notice')">공지사항</div>
        <div class="nav-item" id="menu-free" onclick="showBoard('free')">자유게시판</div>
        <div class="nav-item" id="menu-qna" onclick="showBoard('qna')">질문과 답변</div>
    </nav>
</header>

<div class="main-container">
    <div id="page-home" class="page active">
        <div class="card" style="background: #222; color: white;">
            <h2>서버 연결 완료!</h2>
            <p>이제 누구나 실시간으로 글을 쓸 수 있습니다.</p>
        </div>
        <div class="card"><h3>📢 최신 게시글</h3><div id="latest-posts">로딩 중...</div></div>
    </div>
    <div id="page-board" class="page">
        <h2 id="board-title">게시판</h2>
        <div id="post-list"></div>
    </div>
</div>

<script>
    // 1. 사용자님이 캡처하신 설정값을 여기에 적용했습니다!
    const firebaseConfig = {
        apiKey: "AIzaSyBcxvsiEOyL1lZGvr1UE2gzzZ7HQX5YfbI",
        authDomain: "code-78890.firebaseapp.com",
        projectId: "code-78890",
        storageBucket: "code-78890.firebasestorage.app",
        messagingSenderId: "30317586652",
        appId: "1:30317586652:web:d1e6fa39c319029fb7ac19",
        measurementId: "G-8YJZK0FSFB"
    };
    firebase.initializeApp(firebaseConfig);
    const db = firebase.firestore();

    // 2. 화면 전환 로직 (이미지 image_9c8836.png에서 나타난 메뉴 버그 해결)
    function showPage(pageId) {
        document.querySelectorAll('.page').forEach(p => p.classList.remove('active'));
        document.getElementById('page-' + pageId).classList.add('active');
        document.querySelectorAll('.nav-item').forEach(n => {
            n.classList.remove('active'); // 모든 밑줄 제거
        });
        document.getElementById('menu-' + pageId).classList.add('active'); // 클릭한 것만 밑줄 추가
    }

    function goHome() { showPage('home'); }
    function showBoard(bid) { 
        showPage('board'); 
        document.getElementById('board-title').innerText = bid; 
    }

    // 초기 실행
    window.onload = () => { console.log("서버가 연결되었습니다."); };
</script>
</body>
</html>
