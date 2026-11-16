<script>
// @ts-nocheck

let show;
let speed = $state(50);
$effect(() => {

console.log(show)
const ctx = show.getContext("2d")
show.height = 600
show.width = 600
const pressed = {}
window.addEventListener("keydown",(event) => {
pressed[event.code] = true
})
window.addEventListener("keyup",(event) => {
pressed[event.code] = false
})
function bgclr() {
  const bodyElement = document.body;

  const computedStyle = window.getComputedStyle(bodyElement);
  return computedStyle.backgroundColor;
}
function clear(){
	ctx.fillStyle = bgclr()
	ctx.fillRect(0,0,show.width,show.height)
}
function pixel({x,y}){
	ctx.fillStyle = "red"
	const s = 7
	ctx.fillRect(x- s/2,y - s/2,s,s)
}
function line(a,b){
	ctx.lineWidth = 2
	ctx.strokeStyle = "green"
	ctx.beginPath()
	ctx.moveTo(a.x,a.y)
	ctx.lineTo(b.x,b.y)
	ctx.stroke()
}	
function line2(a,b) {
	ctx.lineWidth = 1
	ctx.strokeStyle = "blue"
	ctx.beginPath()
	ctx.moveTo(a.x,a.y)
	ctx.lineTo(b.x,b.y)
	ctx.stroke()
}
function normal(a){
	return {
		x: (a.x + 1) / 2 * show.width,
		y: (1 - (a.y + 1) / 2) * show.height
	}
}
const perspective = ({x,y,z}) => {return {x: x/z, y: y/z}}
const distance = ({x,y,z}, dz) => {return {x, y, z: z + dz}}
const rotatey = ({x,y,z}, yangle) => {
	return {x:  x * Math.cos(yangle) - z * Math.sin(yangle),
		y,
                z:  x * Math.sin(yangle) + z * Math.cos(yangle)}
}
const rotatex = ({x,y,z}, xangle) => {
	return {x,  
		y:  y * Math.cos(xangle) - z * Math.sin(xangle),
                z:  y * Math.sin(xangle) + z * Math.cos(xangle)}
}
const points = [
	{x: -0.25, y:  0.25, z: 0.25},
	{x:  0.25, y:  0.25, z: 0.25},
	{x:  0.25, y: -0.25, z: 0.25},
	{x: -0.25, y: -0.25, z: 0.25},

	{x: -0.25, y:  0.25, z:-0.25},
	{x:  0.25, y:  0.25, z:-0.25},
	{x:  0.25, y: -0.25, z:-0.25},
	{x: -0.25, y: -0.25, z:-0.25},
]
const tripoints = [
	{x:  0   , y:  0.25, z: 0   },
	{x:  0.25, y: -0.25, z: 0.25},
	{x: -0.25, y: -0.25, z: 0.25},

	{x:  0.25, y: -0.25, z:-0.25},
	{x: -0.25, y: -0.25, z:-0.25},
]
const trifaces = [
	[0,1,2],
	[0,3,4],
	[0,1,3],
	[0,2,4]
]
const faces = [
	[0,1,2,3],
	[4,5,6,7],
	[0,4],
	[1,5],
	[2,6],
	[3,7],
]

const fps = 60
let dz = 1
let yangle = 0
let xangle = 0
function loop(){
	const dt = 1/fps*(speed*0.02)
//	dz += 1*dt
//	yangle += Math.PI*dt
	clear()
//	for (const point of points){
//	pixel(normal(perspective(distance(rotatey(point,yangle), dz))))
//	}
//	line2(normal({x:-1,y:0}),normal({x:1,y:0}))
	const anyKeyPressed =
		pressed["KeyA"] || pressed["KeyD"] || pressed["KeyW"] || pressed["KeyS"];

	if (anyKeyPressed) {
		if (pressed["KeyA"]) yangle += Math.PI * dt;
		if (pressed["KeyD"]) yangle -= Math.PI * dt;
		if (pressed["KeyW"]) xangle += Math.PI * dt;
		if (pressed["KeyS"]) xangle -= Math.PI * dt;
	} else {
	
		yangle += (Math.PI * 0.5) * dt;
		xangle += (Math.PI * 0.25) * dt;
	}
	for (const face of faces) {
		for (let i = 0; i < face.length; i++) {
			const a = points[face[i]]
			const b = points[face[(i+1)%face.length]]
			line(
			normal(perspective(distance(rotatex(rotatey(a,yangle),xangle), dz))),
			normal(perspective(distance(rotatex(rotatey(b,yangle),xangle), dz)))
			)
		}
	}
	setTimeout(loop,1000/fps)
}

setTimeout(loop,1000/fps)
});
</script>
<label for="volume" class="p-7 pb-0">Speed: {speed}</label>
<input type="range" min="0" max="100"bind:value={speed} />
<canvas bind:this={show}></canvas>

