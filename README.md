# Brainwave_Matrix_Intern-
Task1 - To Do List using web technologies like HTML,CSS, Javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>To Do List - Gayatri Pardeshi</title>
    <link rel="shortcut icon" href="images/book.png" type="image/x-icon">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <div class="container">
        <div class="todo-app">
            <h2>TO-DO List <img src="images/book.png" alt="book"></h2>
            <div class="row">
                <input type="text"  id="input-box" placeholder="Add your text">
                <button type="submit" onclick="addTask()">Add</button>
            </div>
            <ul id="list-container">
                <!-- <li class="check">Task 1</li>
                <li>Task 2</li>
                <li>Task 3</li> -->
            </ul>
        </div>
    </div>

    <footer>
        <p>© 2025-2026. All Right Reserved. Designed and Developed by Gayatri Pardeshi</p>
    </footer>

    <script src="script.js"></script>
    
</body>
</html>


*{
    margin: 0;
    padding: 0;
    font-family: 'Poppies',sans-serif;
    box-sizing: border-box;
    overflow-x: hidden;
}

.container{
    width: 100%;
    min-height: 100vh;
    background: linear-gradient(135deg,#153677,#4c085f);
    padding: 10px;
}

.todo-app{
    width: 100%;
    max-width: 540px;
    background: white;
    margin: 100px auto 20px;
    padding: 40px 30px 70px;
    border-radius: 10px;
}

.todo-app h2{
    color: #002765;
    display: flex;
    align-items: center;
    margin-bottom:20px ;
}

.todo-app h2 img{
    width: 30px;
    margin-left: 5px;
}

input{
    flex: 1;
        /*  flex:1 will takes the full width*/
    border: none;
    outline: none;
    background: transparent;
    padding: 10px;
    font-weight: 14px;
}

@media(min-width:546px){
    .row{
        display: flex;
        align-items: center;
        justify-content: space-between;
        background: #edeef0;
        border-radius: 30px;
        padding-left: 20px;
        margin-bottom: 25px;
    } 
    button{
        margin-bottom: 0px;
    }
}

button{
    border: none;
    outline: none;
    padding: 10px 40px;
    background: #77c665;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    border-radius: 40px;
    margin-bottom: 5px;
}

ul li{
    list-style: none;
    font-size: 17px;
    padding: 12px 8px 12px 50px;
    user-select: none;
    cursor: pointer;
    position: relative;
    overflow-y: hidden;
}

ul li::before{
    content: '';
    position: absolute;
    height: 20px;
    width: 20px;
    border: 2px black solid;
    border-radius: 50%;
    /* background-image: url(images/uncheck.png); */
    background-size: cover;
    background-position: center ;
    top: 12px;
    left: 8px;
}

ul li.check{
    color: #555;
    text-decoration: line-through;
}

ul li.check::before{
    background-image: url(images/check-button.png);
}

ul li span{
    position: absolute;
    right: 0;
    top: 5px;
    width: 40px;
    height: 40px;
    font-size: 22px;
    color: #555;
    line-height: 40px;
    text-align: center;
    border-radius: 50%;
}

ul li span:hover{
    background-color: #cdeef0;
}

footer p{
    font-size: 20px;
    text-align: center;
    color: #fff;
    padding-bottom: 10px;
    background: linear-gradient(135deg,#153677,#4c085f);
}


const inputBox=document.getElementById("input-box");
const listContainer=document.getElementById("list-container");

function addTask(){
    if(inputBox.value === ''){
        alert("Please input the text !! and try again");
    }
    else{
        let li=document.createElement("li")
        li.innerHTML = inputBox.value;
        listContainer.appendChild(li);
        let span =document.createElement('span');
        span.innerHTML='\u00d7';
        li.appendChild(span);
    }
    inputBox.value = "";
    saveData();
}

listContainer.addEventListener("click",function(e){
   if(e.target.tagName === "LI"){
    e.target.classList.toggle("check");
    saveData();
   }
   else if(e.target.tagName == "SPAN"){
    e.target.parentElement.remove();
    saveData();
   }
} ,false);

function saveData(){
    localStorage.setItem("data",listContainer.innerHTML);
}

function showTask(){
    listContainer.innerHTML = localStorage.getItem("data");
}
showTask();
