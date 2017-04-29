---
title: guessinggame
date: 2017-04-29 17:24:11
tags: tinygame
---
<html><head><title>guessinggame</title>
<script>
window.onload = newgame;
window.onpopstate = popState;
var state, ui;

function newgame(playagain) {
ui = {
heading: null,

#  at the top of the document.
prompt: null,
input: null,
low: null,
mid: null,
high: null
};
for(var id in ui) ui[id] = document.getElementById(id);

ui.input.onchange = handleGuess;

state = {
n: Math.floor(99 * Math.random()) + 1,
low: 0,
high: 100,
guessnum: 0,
guess: undefined
};

display(state);  
if (playagain === true) save(state);
}

function save(state) {  
if (!history.pushState) return;

var url = "#guess" + state.guessnum;
history.pushState(state,
"",
url);
}

function popState(event) {
if (event.state) {
state = event.state;
display(state);
}
else {
history.replaceState(state, "", "#guess" + state.guessnum);
}
};

function handleGuess() {
var g = parseInt(this.value);
if ((g > state.low) && (g < state.high)) { 
if (g < state.n) state.low = g;          
else if (g > state.n) state.high = g;
state.guess = g;
state.guessnum++;
save(state);
display(state);
}
else {
alert("Please enter a number greater than " + state.low +
" and less than " + state.high);
}
}

function display(state) { 
ui.heading.innerHTML = document.title =
"I'm thinking of a number between " +
state.low + " and " + state.high + ".";

ui.low.style.width = state.low + "%";
ui.mid.style.width = (state.high-state.low) + "%";
ui.high.style.width = (100-state.high) + "%";

ui.input.style.visibility = "visible"; 
ui.input.value = "";
ui.input.focus();

if (state.guess === undefined)
ui.prompt.innerHTML = "Type your guess and hit Enter: ";
else if (state.guess < state.n)
ui.prompt.innerHTML = state.guess + " is too low. Guess again: ";
else if (state.guess > state.n)
ui.prompt.innerHTML = state.guess + " is too high. Guess again: ";
else {
ui.input.style.visibility = "hidden";  // No more guesses now
ui.heading.innerHTML = document.title = state.guess + " is correct! ";
ui.prompt.innerHTML =
"

Congratulations!
<button onclick='newgame(true)'>Play Again</button>";
}
}
</script>
<style>  /* CSS styles to make the game look good */
#prompt { font-size: 16pt; }
table { width: 90%; margin:10px; margin-left:5%; }
#low, #high { background-color: lightgray; height: 1em; }
#mid { background-color: green; }
p { 
text-align: center;
font-size: 50px;
text-shadow: 1px 1px 3px white, 2px 3px 6px magenta, 4px 5px 9px white, 6px 7px 12px magenta;
color: magenta;
}
</style>
</head>
<body>
<h1 id="heading">I'm thinking of a number...
<table><tr><td id="low"></td><td id="mid"></td><td id="high"></td></tr></table>
<label id="prompt"></label><input id="input" type="text">
</body></html>
