<template>
    <div class="canvas-component">
        <div class="canvas-class"></div>
        <canvas></canvas>
        <main>
              <input type="color" class="color-picker">

            <button class="clear">X</button>
        </main>
    </div>
</template>

<script>
export default {
    name: 'Canvas',
    data: function(){
    return{
      color: 'blue'
    }
  },
    methods: {
        changeColor: function (newColor){
          this.color = newColor
        }
    },
    mounted(){
        const clearButton = document.querySelector('.clear');

        const canvas = document.querySelector('canvas');
        const ctx = canvas.getContext('2d');
        const colorPicker = document.querySelector('.color-picker');

        let isDrawing = false;

        console.log(colorPicker.value)

        canvas.addEventListener('mousedown', start);
        canvas.addEventListener('mousemove', draw);
        canvas.addEventListener('mouseup', stop);

        clearButton.addEventListener('click', clearCanvas);

        function start (e) {
          isDrawing = true;
          draw(e);
        }

        function draw ({clientX: x, clientY: y}) {
          if (!isDrawing) return;
          ctx.lineWidth = 3;
          ctx.lineCap = "round";
          ctx.strokeStyle = colorPicker.value;

          ctx.lineTo(x, y);
          ctx.stroke();
          ctx.beginPath();
          ctx.moveTo(x, y);
        }

        function stop () {
          isDrawing = false;
          ctx.beginPath();
        }

        function clearCanvas () {
          ctx.clearRect(0, 0, canvas.width, canvas.height);
        }

        window.addEventListener('resize', resizeCanvas);
        function resizeCanvas () {
          canvas.width = window.innerWidth;
          canvas.height = window.innerHeight;
        }
        resizeCanvas();
            }
        }
</script>

<style>
body{
    margin:0;
    padding:0;
    width:100vw;
    height:100vh;
    background:#F3F3F3;
    font-family:'Roboto', 'Helvetica', sans-serif;
    display: flex;
}

main{
    position:absolute;
    display: flex;
    flex-direction: column;
    align-items: center;
    top:0;
    bottom:0;
    width:100px;
    background:#33384A;
}

main input{
    border: none;
    background-color:#33384A;
    color:white;
    outline:none;
    padding: 0px;
    margin: 30px;
}

.canvas-component{
    display: flex;
    width: 100%;
    justify-content: flex-end;
}

main section{
    display:block;
    margin:15px auto;
    width:30px;
    height:30px;
}

main .colors{
    background:#171717;
    border:1px solid #F3F3F3;
    position:relative;
}

main .clear{
    display:inline;
    width: 30px;
    height:30px;
    margin:0 auto;
    color:#33384A;
    font-size:20px;
    font-weight:900;
    background-color:white;
    border:none;
    outline:none;
    cursor:pointer;
}

main .clear:hover{
        transform: none;
  transition: none;
  filter: none;
}
</style>
