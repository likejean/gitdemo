var world = [
    [1,1,1,1,1,1,1,1,1,1,1,1],
    [1,0,0,0,0,0,2,0,0,0,0,1],
    [1,0,1,1,1,0,1,1,0,1,0,1],
    [1,0,1,1,1,0,1,1,2,1,2,1],
    [1,0,0,2,0,0,2,0,0,0,0,1],
    [1,0,1,1,1,0,1,1,1,1,0,1],
    [1,0,1,1,1,0,1,1,1,1,3,1],
    [1,0,0,0,0,0,2,0,0,0,2,1],
    [1,0,1,1,1,0,1,1,0,1,0,1],
    [1,0,3,1,1,0,0,0,0,1,0,1],
    [1,0,1,1,1,0,1,1,1,1,0,1],
    [1,2,0,0,0,0,0,2,0,0,0,1],
	[1,1,1,1,1,1,1,1,1,1,1,1],
    ];


var worldDict = {
    0: 'blank',
    1: 'wall',
	2: 'money',
	3: 'diamond',
};



function createWorld (){
    var w_output = ""; 
    for (var row = 0; row < world.length; row++)
    {
        w_output += "<div class = 'row'>";
        for (var x = 0; x < world[row].length; x++)       
        {
            w_output += "<div class = ' " + worldDict[world[row][x]] + " '></div>";
        }
        w_output += "</div>";
    }
    
    document.getElementById("world").innerHTML = w_output;
    
    
    
}
createWorld();

var Warrior = {
    x: 1,
    y: 1
};


function WarriorPath(){
    document.getElementById("character").style.top = Warrior.y * 85 + 'px';
    document.getElementById("character").style.left = Warrior.x * 85 + 'px';
}

WarriorPath();



var LeftValue = 85, TopValue = 85, walkValue = 1, Score = 0, kills = 0;
document.getElementById("demo").innerHTML = 'SCORE:' + ' ' + Score + ' ' + '$' + ' - ' + 'KILLS:' + ' ' + kills;

document.onkeydown = function(e){
    console.log(e);
	if (walkValue == 1) {
		walkValue = 2;
	}
	else if (walkValue == 2){
		walkValue = 1;
	}
    
	if(e.keyCode == 37) {
        LeftValue = LeftValue - 85;
      
		document.getElementById("character").style.left = LeftValue+"px";
        document.getElementById("character").style.backgroundImage = "url('left"+walkValue+".png')";
       
       
        if(world[Warrior.y][Warrior.x-1] != 1){
			Warrior.x--;
				if(world[Warrior.y][Warrior.x] == 2){
					world [Warrior.y][Warrior.x] = 0;
					Score++;				
					createWorld();
				}
				else if(world[Warrior.y][Warrior.x] == 3){
					world [Warrior.y][Warrior.x] = 0;
					Score+=5;				
					createWorld();				
				}
			}
				
        }
    
    if(e.keyCode == 39){
        LeftValue = LeftValue + 85;
       
		document.getElementById("character").style.left = LeftValue+"px";
        document.getElementById("character").style.backgroundImage = "url('right"+walkValue+".png')";
        
        
        if(world[Warrior.y][Warrior.x+1] != 1){
			Warrior.x++;           
				if(world[Warrior.y][Warrior.x] == 2){
					world [Warrior.y][Warrior.x] = 0;
					Score++;				
					createWorld();
				}
				else if(world[Warrior.y][Warrior.x] == 3){
					world [Warrior.y][Warrior.x] = 0;
					Score+=5;				
					createWorld();				
				}
            }
    }
	
    if (e.keyCode == 40){
        TopValue = TopValue + 85;
     
		document.getElementById("character").style.top = TopValue+"px";
        document.getElementById("character").style.backgroundImage = "url('down"+walkValue+".png')";
        
        if(world[Warrior.y+1][Warrior.x] != 1){
			Warrior.y++;
            
				if(world[Warrior.y][Warrior.x] == 2){
					world [Warrior.y][Warrior.x] = 0;
					Score++;				
					createWorld();
				}
				else if(world[Warrior.y][Warrior.x] == 3){
					world [Warrior.y][Warrior.x] = 0;
					Score+=5;				
					createWorld();				
				}
            }
    }
	
    else if (e.keyCode == 38){
        TopValue = TopValue - 85;
        
		document.getElementById("character").style.top = TopValue+"px";
        document.getElementById("character").style.backgroundImage = "url('top"+walkValue+".png')";
       
        if(world[Warrior.y-1][Warrior.x] != 1){
			Warrior.y--;
           		if(world[Warrior.y][Warrior.x] == 2){
					world [Warrior.y][Warrior.x] = 0;
					Score++;				
					createWorld();
				}
				else if(world[Warrior.y][Warrior.x] == 3){
					world [Warrior.y][Warrior.x] = 0;
					Score+=5;				
					createWorld();				
				}
			}
		
	}
		
	document.getElementById("demo").innerHTML = 'SCORE:' + ' ' + Score + ' ' + '$' + ' - ' + 'KILLS:' + ' ' + kills;
    WarriorPath();
    
}



var Monster = [
		{x: 10, y: 1, img: 'url("monster.jpg")'},
		{x: 10, y: 11,  img: 'url("monster.jpg")'},
		{x: 10, y: 4,  img: 'url("monster.jpg")'}
		];
		
function MoveMonsters() {  
		var content = "";
	
	for (var index = 0; index < Monster.length; index++){
		
		content += "<div class = 'monster' style = 'background-image:" + Monster[index].img + "; left:" + Monster[index].x*85 + "px; top:" + Monster[index].y*85 + "px;'></div>";
		
//Straights	 - 1
		if(world[Monster[index].y+1][Monster[index].x] != 1 && world[Monster[index].y-1][Monster[index].x] != 1 &&
		world[Monster[index].y][Monster[index].x+1] == 1 && world[Monster[index].y][Monster[index].x-1] == 1)
		{
			if (Monster[index].y > Warrior.y){
				Monster[index].y -= 1;
			}
			else if (Monster[index].y < Warrior.y) {
				Monster[index].y += 1;
			}		
						
			
		}
		//2
		else if(world[Monster[index].y+1][Monster[index].x] == 1 && world[Monster[index].y-1][Monster[index].x] == 1 && 
		world[Monster[index].y][Monster[index].x+1] != 1 && world[Monster[index].y][Monster[index].x-1] != 1)
		{
			if (Monster[index].x > Warrior.x){
				Monster[index].x -= 1;
			}
			else if (Monster[index].x < Warrior.x) {
				Monster[index].x += 1;
			}
			
		}
//Angles - 3		
		else if(world[Monster[index].y-1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x+1] == 1 && 			
			world[Monster[index].y+1][Monster[index].x-1] == 1) 
		{
			if (Monster[index].y >= Warrior.y){
				Monster[index].x -= 1;
			}
			else if (Monster[index].y < Warrior.y) {
				Monster[index].y += 1;
			}
			
		}
		//4
		else if(world[Monster[index].y+1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x-1] == 1 && 
			world[Monster[index].y-1][Monster[index].x+1] == 1) 
		{
			if (Monster[index].y > Warrior.y ){
				Monster[index].y -= 1;
			}
			else if (Monster[index].y <= Warrior.y) {
				Monster[index].x += 1;
			}
			
		}
	 //5
		else if(world[Monster[index].y+1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x+1] == 1 && 
			world[Monster[index].y-1][Monster[index].x-1] == 1)  
		{
			if (Monster[index].y > Warrior.y){
				Monster[index].y -= 1;
			}
			else if (Monster[index].y <= Warrior.y) {
				Monster[index].x -= 1;
			}
			
			
		}
		//6
		else if(world[Monster[index].y-1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x-1] == 1 && 
			world[Monster[index].y+1][Monster[index].x+1] == 1)
		{
			if (Monster[index].y < Warrior.y){
				Monster[index].y += 1;
			}
			else if (Monster[index].y <= Warrior.y) {
				Monster[index].x += 1;
			}
		}
// Dead Ends	7	
		else if(world[Monster[index].y-1][Monster[index].x] == 1 && world[Monster[index].y+1][Monster[index].x] == 1 && 
			world[Monster[index].y][Monster[index].x+1] == 1)  
		{
			Monster[index].x -= 1;
			
			
		}
//8
		else if(world[Monster[index].y-1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x-1] == 1 && 
			world[Monster[index].y][Monster[index].x+1] == 1)  
		{
			Monster[index].y += 1;
			
			
		}
//9
		else if(world[Monster[index].y-1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x-1] == 1 && 
			world[Monster[index].y+1][Monster[index].x] == 1)  
		{
			Monster[index].x += 1;
			
			
		}
//10
		else if(world[Monster[index].y+1][Monster[index].x] == 1 && world[Monster[index].y][Monster[index].x-1] == 1 && 
			world[Monster[index].y][Monster[index].x+1] == 1)  
		{
			Monster[index].x -= 1;
			
			
		} 
// Tees 11
		else if(world[Monster[index].y][Monster[index].x+1] == 1 && world[Monster[index].y-1][Monster[index].x-1] == 1 && 
			world[Monster[index].y+1][Monster[index].x-1] == 1)
		{
			if (Monster[index].x > Warrior.x){
				Monster[index].x -= 1;
			}
			else if (Monster[index].y <= Warrior.y && Monster[index].x <= Warrior.x) {
				Monster[index].y += 1;
			}
			else if (Monster[index].y >= Warrior.y && Monster[index].x <= Warrior.x) {
				Monster[index].y -= 1;
			}
		}
 //      12
		else if(world[Monster[index].y][Monster[index].x-1] == 1 && world[Monster[index].y+1][Monster[index].x+1] == 1 && 
			world[Monster[index].y-1][Monster[index].x+1] == 1)
		{
			if (Monster[index].x < Warrior.x){
				Monster[index].x += 1;
			}
			else if (Monster[index].y >= Warrior.y && Monster[index].x >= Warrior.x) {
				Monster[index].y -= 1;
			}
			else if (Monster[index].y <= Warrior.y && Monster[index].x >= Warrior.x) {
				Monster[index].y += 1;
			}
		}
// 13
		else if(world[Monster[index].y+1][Monster[index].x+1] == 1 && world[Monster[index].y+1][Monster[index].x-1] == 1 && 
			world[Monster[index].y-1][Monster[index].x] == 1)
		{
			if (Monster[index].y >= Warrior.y && Monster[index].x <= Warrior.x ){
				Monster[index].x += 1;
			}
			else if (Monster[index].y < Warrior.y) {
				Monster[index].y += 1;
			}
			else if (Monster[index].y >= Warrior.y && Monster[index].x >= Warrior.x){
				Monster[index].x -= 1;
			}
		}
//14
		else if(world[Monster[index].y+1][Monster[index].x] == 1 && world[Monster[index].y-1][Monster[index].x-1] == 1 && 
			world[Monster[index].y-1][Monster[index].x+1] == 1)
		{
			if (Monster[index].y <= Warrior.y && Monster[index].x >= Warrior.x ){
				Monster[index].x -= 1;
			}
			else if (Monster[index].y > Warrior.y) {
				Monster[index].y -= 1;
			}
			else if (Monster[index].y <= Warrior.y && Monster[index].x <= Warrior.x){
				Monster[index].x += 1;
			}
		}

//CROSS
		else if(world[Monster[index].y+1][Monster[index].x+1] == 1 && world[Monster[index].y-1][Monster[index].x-1] == 1 && 
			world[Monster[index].y-1][Monster[index].x+1] == 1 && world[Monster[index].y+1][Monster[index].x-1] == 1)
		{
			if (Monster[index].y <= Warrior.y && Monster[index].x < Warrior.x ){
				Monster[index].x += 1;
			}
			else if (Monster[index].y >= Warrior.y && Monster[index].x > Warrior.x) {
				Monster[index].x -= 1;
			}
			else if (Monster[index].x >= Warrior.x && Monster[index].y < Warrior.y){
				Monster[index].y += 1;
			}
			else if (Monster[index].x <= Warrior.x && Monster[index].y > Warrior.y){
				Monster[index].y -= 1;
			}
		}
		if (Monster[index].y == Warrior.y && Monster[index].x == Warrior.x){
			kills +=1;
			document.getElementById("demo").innerHTML = 'SCORE:' + ' ' + Score + ' ' + '$' + ' - ' + 'KILLS:' + ' ' + kills;
		
		}

	}
	document.getElementById("monsters").innerHTML = content;
	

	
}


		
function Loop (){    
	MoveMonsters();      
	setTimeout(Loop,500);      

}

	Loop();







