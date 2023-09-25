# omgim

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
