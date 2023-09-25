# omgim

todo.html

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">

    <title>Document</title>
</head>
<body>
    <div>
        <h2><del>나의 할 일 - 이동언</del></h2>
        <hr>
        <div>
            <input id="item" class="form_control" type="text" placeholder="새로운 할 일을 입력하세요">
            <button id="newBtn" type="button" class="btn btn-info" onclick="addItem()">새로운 할 일</button>
        </div>
        <hr>
        <ul id="todolist" class="list-group"></ul>
    </div>
    <script src="todo.js"></script>
</body>
</html>

----------------------------------------

todo.js

function addItem(){
    let list = document.getElementById('todolist')
    let todo = document.getElementById('item')
    let listitem = document.createElement('li')

    let xbtn = document.createElement('button')

    listitem.className = 'list-group-item list-group-item-action list-group-item-warning'
    xbtn.className = 'close'
    xbtn.innerHTML = '삭제'
    xbtn.onclick = function(e){
        let pnode = e.target.parentNode
        list.removeChild(pnode)
    }

    listitem.innerText = todo.value;
    listitem.appendChild(xbtn)

    list.appendChild(listitem)

    todo.value=''
    todo.focus()
}

-------------------------------------------
openweather.html

<!DOCTYPE html>
<html lang="en">

  <head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css">
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="https://code.jquery.com/jquery-3.7.1.js"></script>

    <title>My Weather App</title>
  </head>

  <body>
    <div class="container w-75 mt-5 p-5 shadow text-center bg-warning text-dark">
      <H2>Current Weather in Seoul, Korea</H2>
      <hr>
      <div class="row bg-success p-5 rounded-circle">
        <div class="col-5">
          <img id="icon">
        </div>
        <div class="col-7 m-auto">
          <h1 class="display-3" id="temp"></h1>
          <strong id="weather"></strong><br> 
          Min: <span id="min"></span>°C, Max: <span id="max"></span>°C<br> 
          Wind: <span id="wind"></span>m/s
        </div>
      </div>
    </div>

    <h3>도시 입력</h3>
    <input type="text" id="city" class="form-control">

    <h3>온도표시 옵션</h3>
    <select id="tempshow" class="form-control">
      <option value="standard"> 절대온도 </option>
      <option value="metric" selected> 섭씨 </option>
      <option value="imperial"> 화씨 </option>
    </select>


    <h3>언어표시 옵션</h3>
    <select id="langshow" class="form-control">
      <option value="en" > 영어 </option>
      <option value="zh" selected> 중국어 </option>
      <option value="ja"> 일어 </option>
      <option value="kr"> 한국어 </option>
    </select>

    <input type="button" id="go" value="날씨 검색" class="btn-print">




    <script src="openweather.js"></script>
  </body>

</html>

openweather.js

let temp = document.querySelector('#temp');
let min = document.querySelector('#min');
let max = document.querySelector('#max');
let wind = document.querySelector('#wind');
let weather = document.querySelector('#weather');
let icon = document.querySelector("#icon");
let icon_url = "https://openweathermap.org/themes/openweathermap/assets/vendor/owm/img/widgets/";

axios.get('https://api.openweathermap.org/data/2.5/find?q=Seoul&units=metric&appid=7d96bc5108f52b80e2d9075a369b9f35')
  .then(function(response) {
    console.log(response.data);
    let wdata = response.data.list[0];
    let exdata = response.data.list[0].weather[0];

    temp.innerText = wdata.main.temp + "°C";
    min.innerText = wdata.main.temp_min;
    max.innerText = wdata.main.temp_max;
    wind.innerText = wdata.wind.speed;

    weather.innerText = exdata.main + "," + exdata.description;
    icon.setAttribute('src', icon_url + exdata.icon + ".png");
  })
  .catch(function(error) {
    console.log(error);
  })
  .then(function() {});

  function getweather(cityname, tempdisplay, langdisply){
    apiorigin = 'https://api.openweathermap.org/data/2.5/find?appid=7d96bc5108f52b80e2d9075a369b9f35'
  
    apistring = apiorigin + "&q=" + cityname + "&units=" + tempdisplay + "&lang=" + langdisply

    axios.get(apistring)
  .then(function(response) {
    console.log(response.data);
    let wdata = response.data.list[0];
    let exdata = response.data.list[0].weather[0];

    temp.innerText = wdata.main.temp + "°C";
    min.innerText = wdata.main.temp_min;
    max.innerText = wdata.main.temp_max;
    wind.innerText = wdata.wind.speed;

    weather.innerText = exdata.main + "," + exdata.description;
    icon.setAttribute('src', icon_url + exdata.icon + ".png");
  })
  .catch(function(error) {
    console.log(error);
  })
  .then(function() {});
  }

  const button = document.getElementById("go")
  button.onclick = function(e){
    cityinput = document.getElementById("city")
    cityname = cityinput.value

    unitinput = document.getElementById("tempshow")
    unitselect = unitinput.value

    langinput = document.getElementById("langshow")
    langselect = langinput.value
    getweather(cityname, unitselect, langselect)
  }

  let WeatherObject = {
    getWeather: function() {

      alert("$.ajax 실행")

      $.ajax({
        type: "GET",
        url: 'https://api.openweathermap.org/data/2.5/weather?q=Seoul&units=metric&appid=7d96bc5108f52b80e2d9075a369b9f35',
      }).done(function(response) {
              let wdata = response
              let exdata = response.weather[0];
          
              temp.innerText = wdata.main.temp + "°C";
              min.innerText = wdata.main.temp_min;
              max.innerText = wdata.main.temp_max;
              wind.innerText = wdata.wind.speed;
          
              weather.innerText = exdata.main + "," + exdata.description;
              icon.setAttribute('src', icon_url + exdata.icon + ".png");
      }).fail(function(error) {
        alert("!/js/user.js에서 에러발생: " + error.statusText);
      });
    },
   }
  
   WeatherObject.getWeather();

   chat.html

   <!DOCTYPE html>
<html lang="en">
<head>
  <title>Bootstrap 5 Website Example</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js"></script>
  <style>
  .fakeimg {
    height: 200px;
    background: #aaa;
  }
  </style>
  <script src="https://code.jquery.com/jquery-3.7.1.js"></script>
</head>
<body>

<div class="p-5 bg-primary text-white text-center">
  <h1>이동언의 인공지능 체험페이지</h1>
  <p>실제로 써봅시다</p> 
</div>
<textarea  id="txtMsg" cols="30" rows="10"></textarea>
<button onclick="Send()" id="btnSend"> textdavinci003보내기 </button>
<textarea  id="txtOut" cols="30" rows="10"></textarea>

<hr>
<textarea  id="imgMsg" cols="30" rows="10"></textarea>
<button onclick="Draw()" id="btnDraw">이미지생성</button>

<hr>
<img id="gimage" style="border:5px solid#555" >
<img id="gimage2" style="border:5px solid#a21414" >
<script src="chat.js"></script>

</body>
</html>

chat.js

var OPENAI_API_KEY = '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'

function Send(){

  var sQuestion = txtMsg.value;
  var data = {
        model: "text-davinci-003",
        prompt: sQuestion,
        max_tokens: 2048,
        temperature: 0
  }  
  $.ajax({
    type: "POST",
    url: 'https://api.openai.com/v1/completions',
    headers:{
        "Accept" : "application/json",
        "Content-Type": "application/json", 
        "Authorization": "Bearer " +  OPENAI_API_KEY },
    data: JSON.stringify(data),

  }).done(function(response) {

        var sanswer = response.choices[0].text
        txtOut.value = sanswer

  }).fail(function(error) {
    alert("!/js/user.js에서 에러발생: " + error.statusText);
    console.log(error)
  });
}

function Draw(){

  var sQuestion = imgMsg.value;
  var data = {
        prompt: sQuestion,
        n:2,
        size: "512x512"
  }  
  $.ajax({
    type: "POST",
    url: 'https://api.openai.com/v1/images/generations',
    headers:{
        "Accept" : "application/json",
        "Content-Type": "application/json", 
        "Authorization": "Bearer " +  OPENAI_API_KEY },
    data: JSON.stringify(data),

  }).done(function(response) {

        gimage.src = response.data[0].url
        gimage2.src = response.data[1].url

  }).fail(function(error) {
    alert("!/js/user.js에서 에러발생: " + error.statusText);
    console.log(error)
  });
}

        
let ChatObject = {
    getAnswer: function() {

      alert("$.ajax 실행")
      var data = {
            model: "text-davinci-003",
            prompt: "강호동이 누구?",
            max_tokens: 2048,
            temperature: 0
      }  
      $.ajax({
        type: "POST",
        url: 'https://api.openai.com/v1/completions',
        headers:{
            "Accept" : "application/json",
            "Content-Type": "application/json", 
            "Authorization": "Bearer " +  OPENAI_API_KEY },
        data: JSON.stringify(data),

      }).done(function(response) {

             console.log(response)
             alert(response.choices[0].text)

      }).fail(function(error) {
        alert("!/js/user.js에서 에러발생: " + error.statusText);
        console.log(error)
      });
    },
   }


  chatboot.html

  <!DOCTYPE html>
<html lang="en">
<head>
  <title>인공지능 체험 사이트</title>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet">
  <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js"></script>
  <style>
  .fakeimg {
    height: 200px;
    background: #aaa;
  }
  </style>
  <script src="https://code.jquery.com/jquery-3.7.1.js"></script>
</head>
<body>

<div class="p-5 bg-primary text-white text-center">
  <h1>이동언의 인공지능 체험페이지</h1>
  <p>실제로 써봅시다</p> 
</div>

<h2>인공지능 대화 체험</h2>

<div class="input-group mb-3">
    <input type="text" class="form-control" placeholder="알고싶은걸 말씀하세요" id="txtMsg">
    <button class="btn btn-success" type="submit" onclick="Send()" id="btnSend">대답하기</button>
  </div>


<textarea  id="txtOut" rows="5" class="form-control" placeholder="답변이 나타나는 곳입니다"></textarea>

<hr>

<h2>인공지능 이미지생성 체험</h2>

<div class="input-group mb-3">
    <input type="text" class="form-control" placeholder="그림에 대해 말씀하세요" id="imgMsg">
    <button class="btn btn-success" type="submit" onclick="Draw()" id="btnSend">대답하기</button>
  </div>

<!-- <textarea  id="imgMsg" cols="30" rows="10"></textarea>
<button onclick="Draw()" id="btnDraw">이미지생성</button> -->

<hr>
<img id="gimage" style="border:5px solid#555" >
<img id="gimage2" style="border:5px solid#a21414" >
<script src="chat.js"></script>

</body>
</html>






