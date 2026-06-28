# doraniige-mu
ドラ兄が作ったゲームです
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>3D Game</title>

<style>
body{
 margin:0;
 overflow:hidden;
}
canvas{
 display:block;
}
</style>

</head>

<body>

<script src="https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.min.js"></script>

<script>

const scene=new THREE.Scene();

scene.background=new THREE.Color(0x87ceeb);


const camera=new THREE.PerspectiveCamera(
75,
innerWidth/innerHeight,
0.1,
1000
);


const renderer=new THREE.WebGLRenderer();

renderer.setSize(
innerWidth,
innerHeight
);

document.body.appendChild(renderer.domElement);


// 地面

let ground=new THREE.Mesh(
new THREE.BoxGeometry(20,0.2,20),
new THREE.MeshBasicMaterial({
color:0x00aa00
})
);

scene.add(ground);


// プレイヤー

let player=new THREE.Mesh(
new THREE.BoxGeometry(1,2,1),
new THREE.MeshBasicMaterial({
color:0xff0000
})
);

player.position.y=1;

scene.add(player);


camera.position.set(
0,3,5
);


// 操作

let keys={};

onkeydown=e=>keys[e.key]=true;
onkeyup=e=>keys[e.key]=false;


function move(){

if(keys["w"])
 player.position.z-=0.1;

if(keys["s"])
 player.position.z+=0.1;

if(keys["a"])
 player.position.x-=0.1;

if(keys["d"])
 player.position.x+=0.1;


camera.position.x=player.position.x;
camera.position.z=player.position.z+5;

camera.lookAt(player.position);

}


function loop(){

requestAnimationFrame(loop);

move();

renderer.render(
scene,
camera
);

}

loop();


</script>

</body>
</html>