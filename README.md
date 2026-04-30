<!DOCTYPE html>
<html lang="ko">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>아트라이프다솜 · H.A.T. 임팩트 기록</title>
<style>
  *{box-sizing:border-box;margin:0;padding:0}
  body{font-family:system-ui,-apple-system,sans-serif;background:#f4f6f3;min-height:100vh;color:#111}
  .header{background:linear-gradient(135deg,#4a7c59 0%,#2d5016 100%);padding:18px 20px 14px}
  .header h1{font-size:17px;font-weight:800;color:#fff}
  .header p{font-size:11px;color:rgba(255,255,255,.7);margin-top:3px}
  .tabs{display:flex;background:#fff;border-bottom:1px solid #e5e7eb}
  .tab{flex:1;padding:11px 4px;font-size:12px;font-weight:700;background:none;border:none;cursor:pointer;border-bottom:3px solid transparent;color:#9ca3af}
  .tab.active{border-bottom-color:#4a7c59;color:#4a7c59}
  .page{display:none;padding:16px;max-width:680px;margin:0 auto}
  .page.active{display:block}
  .card{background:#fff;border-radius:12px;padding:18px 16px;box-shadow:0 1px 6px rgba(0,0,0,.07);margin-bottom:14px}
  .card-title{font-size:14px;font-weight:800;margin-bottom:14px}
  .grid2{display:grid;grid-template-columns:1fr 1fr;gap:12px}
  .span2{grid-column:1/-1}
  label{display:block;font-size:11px;font-weight:700;color:#6b7280;margin-bottom:5px}
  input,select,textarea{width:100%;padding:9px 11px;border:1px solid #e5e7eb;border-radius:7px;font-size:13px;outline:none;background:#fff;font-family:inherit}
  textarea{height:72px;resize:vertical}
  .btn{width:100%;padding:13px;font-size:14px;font-weight:800;border:none;border-radius:8px;cursor:pointer;margin-top:14px}
  .btn-primary{background:#4a7c59;color:#fff}
  .btn-outline{background:#f0fdf4;border:1px solid #4a7c59;color:#4a7c59;font-weight:700;font-size:13px}
  .info-box{background:#fffbeb;border:1px solid #fcd34d;border-radius:8px;padding:11px 14px;font-size:12px;color:#92400e;line-height:1.8;margin-top:12px}
  .toast{position:fixed;top:12px;left:50%;transform:translateX(-50%);padding:10px 20px;border-radius:8px;font-size:13px;font-weight:600;color:#fff;z-index:999;display:none;white-space:nowrap;box-shadow:0 4px 14px rgba(0,0,0,.18)}
  .total-bar{display:grid;grid-template-columns:1fr 1fr 1fr;gap:8px;margin-bottom:14px}
  .total-box{background:#fff;border-radius:9px;padding:12px 8px;text-align:center;box-shadow:0 1px 4px rgba(0,0,0,.06)}
  .total-val{font-size:18px;font-weight:900;color:#4a7c59}
  .total-lbl{font-size:10px;color:#9ca3af;margin-top:2px}
  .filter-row{display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:14px}
  .record-item{background:#fff;border-radius:10px;padding:14px;margin-bottom:10px;box-shadow:0 1px 4px rgba(0,0,0,.06)}
  .tag{display:inline-block;font-size:11px;font-weight:700;padding:2px 8px;border-radius:20px;margin-right:4px;margin-bottom:6px}
  .tag-green{background:#4a7c5920;color:#4a7c59;border:1px solid #4a7c5935}
  .tag-purple{background:#6d28d920;color:#6d28d9;border:1px solid #6d28d935}
  .tag-gray{background:#6b728020;color:#6b7280;border:1px solid #6b728035}
  .rec-date{font-size:13px;font-weight:700}
  .rec-detail{font-size:12px;color:#6b7280;margin-top:4px;line-height:1.6}
  .rec-note{font-size:12px;color:#4b5563;margin-top:7px;padding:7px 10px;background:#f9fafb;border-radius:6px;border-left:3px solid #4a7c59}
  .kpi-grid{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin-bottom:16px}
  .kpi{background:#fff;border-radius:12px;padding:16px 14px;box-shadow:0 1px 6px rgba(0,0,0,.07)}
  .kpi-lbl{font-size:10px;color:#9ca3af;font-weight:700}
  .kpi-val{font-size:28px;font-weight:900;color:#4a7c59;margin-top:6px}
  .kpi-unit{font-size:13px;font-weight:600;color:#6b7280;margin-left:4px}
  .bar-row{margin-bottom:14px}
  .bar-top{display:flex;justify-content:space-between;font-size:12px;margin-bottom:5px}
  .bar-bg{background:#f3f4f6;border-radius:5px;height:8px}
  .bar-fill{background:#6d28d9;height:100%;border-radius:5px;transition:width .5s}
  .calc-box{background:#f0fdf4;border-radius:7px;padding:8px 12px;font-size:13px;color:#4a7c59;font-weight:700;margin-top:12px;display:none}
  .empty{text-align:center;color:#9ca3af;padding:40px;font-size:14px}
  .loading{text-align:center;color:#9ca3af;padding:24px;font-size:13px}
</style>
</head>
<body>

<div class="toast" id="toast"></div>

<div class="header">
  <h1>아트라이프다솜</h1>
  <p>H.A.T. 임팩트 기록 시스템 (2003~) &nbsp;·&nbsp; <span style="background:rgba(255,255,255,.2);padding:1px 8px;border-radius:20px;font-size:10px">🔗 구글 시트 연동</span></p>
</div>

<div class="tabs">
  <button class="tab active" onclick="switchTab('input',this)">➕ 기록 입력</button>
  <button class="tab" onclick="switchTab('records',this)">📋 전체 기록</button>
  <button class="tab" onclick="switchTab('dashboard',this)">📊 임팩트 현황</button>
</div>

<!-- 입력 탭 -->
<div class="page active" id="page-input">
  <div class="card">
    <div style="display:flex;align-items:center;gap:10px;margin-bottom:14px">
      <div class="card-title" style="margin-bottom:0">새 세션 기록</div>
      <span class="tag tag-green" style="font-size:12px">H.A.T.</span>
    </div>
    <div class="grid2">
      <div>
        <label>날짜 *</label>
        <input type="date" id="f-date" min="2003-01-01">
      </div>
      <div>
        <label>주진행 강사 *</label>
        <select id="f-instructor">
          <option value="">선택</option>
          <option>윤현서</option><option>이연정</option><option>김한슬</option><option>안정윤</option>
        </select>
      </div>
      <div class="span2">
        <label>대상 *</label>
        <select id="f-target" onchange="toggleCustomTarget()">
          <option value="">선택</option>
          <option>소방공무원</option>
          <option>전문자원봉사자</option>
          <option>시니어</option>
          <option>성착취피해 여성청소년</option>
          <option>성매매·성폭력피해 여성</option>
          <option value="__custom__">기타 (직접 입력)</option>
        </select>
        <input type="text" id="f-target-custom" placeholder="대상 직접 입력" style="display:none;margin-top:8px">
      </div>
      <div>
        <label>회기 수 *</label>
        <input type="number" id="f-sessionNo" min="1" placeholder="1" oninput="calcTotal()">
      </div>
      <div>
        <label>1회기 시간(분) *</label>
        <input type="number" id="f-sessionMin" min="30" step="30" value="90" oninput="calcTotal()">
      </div>
      <div>
        <label>참여 인원(명) *</label>
        <input type="number" id="f-participants" min="1" placeholder="0">
      </div>
      <div>
        <label>장소</label>
        <input type="text" id="f-location" placeholder="운영 장소">
      </div>
      <div class="span2">
        <label>보조강사 (기록용, 집계 제외)</label>
        <input type="text" id="f-assistant" placeholder="없으면 공백">
      </div>
      <div class="span2">
        <label>임팩트 소감 (선택)</label>
        <textarea id="f-notes" placeholder="성과 기록용 — 참여자의 특별한 반응이나 소감이 있다면 자유롭게 기술해 주세요."></textarea>
      </div>
    </div>
    <div class="calc-box" id="calcBox"></div>
    <button class="btn btn-primary" id="submitBtn" onclick="submitRecord()">기록 저장 + 구글 시트 전송</button>
  </div>
  <div class="info-box">
    💡 <b>중복 카운팅 방지:</b> 주진행 강사만 기록합니다. 보조강사는 참고용, 집계 제외.<br>
    📅 2003년 이후 과거 기록도 해당 날짜 선택 후 입력 → 전체 누적에 자동 반영.
  </div>
</div>

<!-- 기록 탭 -->
<div class="page" id="page-records">
  <div class="filter-row">
    <select id="fy" onchange="renderRecords()"><option value="">전체 연도</option></select>
    <select id="fm" onchange="renderRecords()">
      <option value="">전체 월</option>
      <option>01</option><option>02</option><option>03</option><option>04</option>
      <option>05</option><option>06</option><option>07</option><option>08</option>
      <option>09</option><option>10</option><option>11</option><option>12</option>
    </select>
    <select id="fi" onchange="renderRecords()">
      <option value="">전체 강사</option>
      <option>윤현서</option><option>이연정</option><option>김한슬</option><option>안정윤</option>
    </select>
    <select id="ft" onchange="renderRecords()"><option value="">전체 대상</option></select>
  </div>
  <div class="total-bar">
    <div class="total-box"><div class="total-val" id="t-sessions">-</div><div class="total-lbl">총 회기</div></div>
    <div class="total-box"><div class="total-val" id="t-hours">-</div><div class="total-lbl">총 시간</div></div>
    <div class="total-box"><div class="total-val" id="t-ppl">-</div><div class="total-lbl">총 인원</div></div>
  </div>
  <button class="btn btn-outline" onclick="loadRecords()" style="margin-bottom:10px;margin-top:0">🔄 새로고침</button>
  <button class="btn btn-outline" onclick="exportCSV()" style="margin-bottom:14px;margin-top:4px">📥 CSV 내보내기</button>
  <div id="recordList"><div class="loading">🔄 구글 시트에서 불러오는 중...</div></div>
</div>

<!-- 대시보드 탭 -->
<div class="page" id="page-dashboard">
  <div style="display:grid;grid-template-columns:1fr 1fr;gap:8px;margin-bottom:14px">
    <select id="dy" onchange="renderDashboard()"><option value="">전체 연도 (2003~)</option></select>
    <select id="dm" onchange="renderDashboard()">
      <option value="">전체 월</option>
      <option>01</option><option>02</option><option>03</option><option>04</option>
      <option>05</option><option>06</option><option>07</option><option>08</option>
      <option>09</option><option>10</option><option>11</option><option>12</option>
    </select>
  </div>
  <div class="kpi-grid">
    <div class="kpi"><div class="kpi-lbl">세션 기록 건수</div><div class="kpi-val" id="k-count">-<span class="kpi-unit">건</span></div></div>
    <div class="kpi"><div class="kpi-lbl">누적 회기 수</div><div class="kpi-val" id="k-sessions">-<span class="kpi-unit">회기</span></div></div>
    <div class="kpi"><div class="kpi-lbl">누적 참여 인원</div><div class="kpi-val" id="k-ppl">-<span class="kpi-unit">명</span></div></div>
    <div class="kpi"><div class="kpi-lbl">누적 운영 시간</div><div class="kpi-val" id="k-hours">-<span class="kpi-unit">시간</span></div></div>
  </div>
  <div class="card">
    <div class="card-title">대상별 임팩트 현황</div>
    <div id="targetChart"><div class="loading">불러오는 중...</div></div>
  </div>
</div>

<script>
// ★ Apps Script URL이 여기 고정되어 있습니다
var SCRIPT_URL = 'https://script.google.com/macros/s/AKfycbzCcKVN2VvJzgWD7fQJoVKxtzEp8ZUoz82PbyvylhJxVAMmjx4lfdr-9zGvJQ_0Fy0CZg/exec';

var allRecords = [];

window.onload = function() { loadRecords(); };

function loadRecords() {
  document.getElementById('recordList').innerHTML = '<div class="loading">🔄 구글 시트에서 불러오는 중...</div>';
  fetch(SCRIPT_URL + '?action=getAll')
    .then(function(r){ return r.json(); })
    .then(function(data) {
      if (Array.isArray(data)) {
        allRecords = data.sort(function(a,b){ return new Date(b.date)-new Date(a.date); });
        updateYearFilters();
        updateTargetFilter();
        renderRecords();
        renderDashboard();
      }
    })
    .catch(function(){ showToast('데이터 불러오기 실패. 잠시 후 다시 시도해주세요.', true); });
}

function switchTab(name, el) {
  document.querySelectorAll('.page').forEach(function(p){ p.classList.remove('active'); });
  document.querySelectorAll('.tab').forEach(function(t){ t.classList.remove('active'); });
  document.getElementById('page-'+name).classList.add('active');
  el.classList.add('active');
}

function calcTotal() {
  var n = +document.getElementById('f-sessionNo').value;
  var m = +document.getElementById('f-sessionMin').value;
  var box = document.getElementById('calcBox');
  if (n && m) {
    box.style.display = 'block';
    box.textContent = '✓ 총 운영시간: '+(n*m)+'분 ('+(n*m/60).toFixed(1)+'시간)';
  } else { box.style.display = 'none'; }
}

function toggleCustomTarget() {
  var sel = document.getElementById('f-target');
  document.getElementById('f-target-custom').style.display = sel.value==='__custom__' ? 'block' : 'none';
}

function submitRecord() {
  var date = document.getElementById('f-date').value;
  var instructor = document.getElementById('f-instructor').value;
  var targetSel = document.getElementById('f-target').value;
  var targetCustom = document.getElementById('f-target-custom').value.trim();
  var target = targetSel==='__custom__' ? targetCustom : targetSel;
  var sessionNo = +document.getElementById('f-sessionNo').value;
  var sessionMin = +document.getElementById('f-sessionMin').value;
  var participants = +document.getElementById('f-participants').value;

  if (!date||!instructor||!target||!sessionNo||!participants) {
    showToast('필수 항목(*)을 모두 입력해주세요.', true); return;
  }

  var entry = {
    date:date, instructor:instructor, program:'H.A.T.', target:target,
    sessionNo:sessionNo, sessionMin:sessionMin, totalMin:sessionNo*sessionMin,
    participants:participants,
    location:document.getElementById('f-location').value,
    assistant:document.getElementById('f-assistant').value,
    notes:document.getElementById('f-notes').value
  };

  var btn = document.getElementById('submitBtn');
  btn.textContent='저장 중...'; btn.disabled=true;

  fetch(SCRIPT_URL+'?data='+encodeURIComponent(JSON.stringify(entry)), {mode:'no-cors'})
    .then(function() {
      allRecords.unshift(entry);
      updateYearFilters(); updateTargetFilter();
      resetForm();
      showToast('저장되었습니다. 구글 시트에 전송됨 ✓');
      btn.textContent='기록 저장 + 구글 시트 전송'; btn.disabled=false;
    })
    .catch(function() {
      showToast('전송 실패. 네트워크를 확인해주세요.', true);
      btn.textContent='기록 저장 + 구글 시트 전송'; btn.disabled=false;
    });
}

function resetForm() {
  ['f-date','f-location','f-assistant','f-notes','f-sessionNo','f-target-custom'].forEach(function(id){
    document.getElementById(id).value='';
  });
  document.getElementById('f-instructor').value='';
  document.getElementById('f-target').value='';
  document.getElementById('f-sessionMin').value='90';
  document.getElementById('f-participants').value='';
  document.getElementById('f-target-custom').style.display='none';
  document.getElementById('calcBox').style.display='none';
}

function updateYearFilters() {
  var years=[...new Set(allRecords.map(function(r){return (r.date||'').slice(0,4);}))].filter(Boolean).sort().reverse();
  ['fy','dy'].forEach(function(id){
    var sel=document.getElementById(id);
    var cur=sel.value;
    sel.innerHTML='<option value="">'+(id==='dy'?'전체 연도 (2003~)':'전체 연도')+'</option>';
    years.forEach(function(y){sel.innerHTML+='<option value="'+y+'">'+y+'년</option>';});
    sel.value=cur;
  });
}

function updateTargetFilter() {
  var targets=[...new Set(allRecords.map(function(r){return r.target;}))].filter(Boolean);
  var sel=document.getElementById('ft');
  var cur=sel.value;
  sel.innerHTML='<option value="">전체 대상</option>';
  targets.forEach(function(t){sel.innerHTML+='<option value="'+esc(t)+'">'+esc(t)+'</option>';});
  sel.value=cur;
}

function getFiltered(yId,mId,iId,tId) {
  var fy=document.getElementById(yId).value;
  var fm=document.getElementById(mId).value;
  var fi=iId?document.getElementById(iId).value:'';
  var ft=tId?document.getElementById(tId).value:'';
  return allRecords.filter(function(r){
    if(fy&&(r.date||'').slice(0,4)!==fy)return false;
    if(fm&&(r.date||'').slice(5,7)!==fm)return false;
    if(fi&&r.instructor!==fi)return false;
    if(ft&&r.target!==ft)return false;
    return true;
  });
}

function renderRecords() {
  var filtered=getFiltered('fy','fm','fi','ft');
  var sessions=filtered.reduce(function(a,r){return a+(+r.sessionNo||0);},0);
  var mins=filtered.reduce(function(a,r){return a+(+r.totalMin||0);},0);
  var ppl=filtered.reduce(function(a,r){return a+(+r.participants||0);},0);
  document.getElementById('t-sessions').textContent=sessions+'회기';
  document.getElementById('t-hours').textContent=Math.round(mins/60)+'시간';
  document.getElementById('t-ppl').textContent=ppl.toLocaleString()+'명';

  if(filtered.length===0){
    document.getElementById('recordList').innerHTML='<div class="empty">기록이 없습니다.</div>'; return;
  }
  var html='';
  filtered.forEach(function(r){
    html+='<div class="record-item">';
    html+='<span class="tag tag-green">'+esc(r.instructor)+'</span>';
    html+='<span class="tag tag-purple">'+esc(r.target)+'</span>';
    html+='<span class="tag tag-gray">H.A.T.</span>';
    html+='<div class="rec-date">'+esc(r.date)+'</div>';
    html+='<div class="rec-detail">'+r.sessionNo+'회기 × '+r.sessionMin+'분 = <b>'+r.totalMin+'분</b> · 참여 <b>'+r.participants+'명</b>';
    if(r.location)html+=' · '+esc(r.location);
    if(r.assistant)html+=' <span style="color:#9ca3af">· 보조: '+esc(r.assistant)+'</span>';
    html+='</div>';
    if(r.notes)html+='<div class="rec-note">💬 '+esc(r.notes)+'</div>';
    html+='</div>';
  });
  document.getElementById('recordList').innerHTML=html;
}

function renderDashboard() {
  var filtered=getFiltered('dy','dm','','');
  var sessions=filtered.reduce(function(a,r){return a+(+r.sessionNo||0);},0);
  var mins=filtered.reduce(function(a,r){return a+(+r.totalMin||0);},0);
  var ppl=filtered.reduce(function(a,r){return a+(+r.participants||0);},0);
  document.getElementById('k-count').innerHTML=filtered.length+'<span class="kpi-unit">건</span>';
  document.getElementById('k-sessions').innerHTML=sessions+'<span class="kpi-unit">회기</span>';
  document.getElementById('k-ppl').innerHTML=ppl.toLocaleString()+'<span class="kpi-unit">명</span>';
  document.getElementById('k-hours').innerHTML=Math.round(mins/60)+'<span class="kpi-unit">시간</span>';

  var byTarget={};
  filtered.forEach(function(r){
    if(!byTarget[r.target])byTarget[r.target]={s:0,p:0};
    byTarget[r.target].s+=(+r.sessionNo||0);
    byTarget[r.target].p+=(+r.participants||0);
  });
  var sorted=Object.entries(byTarget).sort(function(a,b){return b[1].p-a[1].p;});
  if(sorted.length===0){document.getElementById('targetChart').innerHTML='<div class="empty">데이터가 없습니다.</div>';return;}
  var html='';
  sorted.forEach(function(entry){
    var t=entry[0],d=entry[1];
    var pct=ppl>0?Math.round(d.p/ppl*100):0;
    html+='<div class="bar-row"><div class="bar-top"><span style="font-weight:700;color:#374151">'+esc(t)+'</span><span style="color:#6b7280">'+d.s+'회기 · <b>'+d.p+'명</b> ('+pct+'%)</span></div><div class="bar-bg"><div class="bar-fill" style="width:'+pct+'%"></div></div></div>';
  });
  document.getElementById('targetChart').innerHTML=html;
}

function exportCSV() {
  var header=['날짜','주진행강사','프로그램명','대상','회기수','1회기(분)','총시간(분)','참여인원','장소','보조강사','임팩트소감'];
  var rows=allRecords.map(function(r){
    return [r.date,r.instructor,r.program||'H.A.T.',r.target,r.sessionNo,r.sessionMin,r.totalMin,r.participants,r.location||'',r.assistant||'',r.notes||'']
      .map(function(v){return '"'+(v||'').toString().replace(/"/g,'""')+'"';}).join(',');
  });
  var a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob(['\uFEFF'+[header.join(',')].concat(rows).join('\n')],{type:'text/csv;charset=utf-8'}));
  a.download='아트라이프다솜_임팩트기록.csv';
  a.click();
}

function esc(s){return (s||'').toString().replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;');}
function showToast(msg,err){
  var t=document.getElementById('toast');
  t.textContent=msg;
  t.style.background=err?'#ef4444':'#4a7c59';
  t.style.display='block';
  setTimeout(function(){t.style.display='none';},3200);
}
</script>
</body>
</html>
