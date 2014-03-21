---
layout: post
title:  "Tic Tac Toe in JavaScript, Part 3 (final version)"
tags: javascript game 
---

In <a href="/2014/03/16/tic-tac-toe-in-javascript-part-2.html">the last post</a> I added a couple of basic strategies to my Tic Tac Toe game that made it less than totally stupid, but still not too hard to beat. If you play that game a few times you'll likely identify a few holes in its logic - tactics you can use to repeatedly beat the computer. In this final version, I've added four more strategies that - I think - prevent the human player from ever winning and take every opportunity given to win. If you can beat the game with all the strategies enabled, please tell me how. Here are the final four strategies. Full source code is at the bottom as a Gist.

### Win Strategy

This is a really obvious one, but something I initially overlooked. The computer player didn't look for an opportunity to win the game in a single turn and take it. This function does that. Its the first strategy attempted.

{% highlight javascript %}
function strategyWin() {
  var isComputer = function(val) { return val==computer; }
  var isBlank = function(val) { return val==''; }
  // look for 2 computer plays and one blank, indicating an immediate win
  var canWin = function(a,b,c) {
    if (matches([a,b,c], isComputer)==2 && 
        matches([a,b,c], isBlank)==1) {
      ret = findInArray([a,b,c], isBlank);
      return true;
    } 
  };
  var ret = -1;
  var ix = -1;
  // search rows
  ix = iterateRows(canWin);
  if (ix>-1 && ret>-1) return [ret, ix];
  // search columns
  ix = iterateCols(canWin);
  if (ix>-1 && ret>-1) return [ix, ret];
  // search diagonals
  ix = iterateDiags(canWin);
  if (ix>-1 && ret>-1) return convertDiag(ix, ret);
  else return false;
}
{% endhighlight %}

### Middle & Middle Defense Strategies

This strategy targets a specific method of winning Tic Tac Toe. You start in the middle and then make a triangle with one in the corner and one on the side. This creates a scenario, unless previously blocked by the opponent, where there are two opportunities to win, and the opponent only has one turn to stop you.

The first of these is the strategy to block the opponent from using this strategy. The second is the strategy to grab the middle space if its available.

{% highlight javascript %}
function strategyMiddleDefense() {
  // if middle is taken, take the first corner
  if (turns==1 && val(1,1)==player) return [0,0];
  else if (turns==3 && val(1,1)==player) {
    if (val(2,0)=='') return [2,0];
    else if (val(0,2)) return [0,2];
    else if (val(2,2)) return [2,2];
    else return false;
  } 
  else return false;
}

function strategyMiddle() {
  if (val(1,1)=='') return [1,1];
  else return false;
}
{% endhighlight %}

### Corner Defense Strategy

This strategy prevents an attack where two adjacent middle sides are taken, followed by the corner between them. Like the middle attack, this creates a situation where there are two simultaneous opportunities for the opponent to win and the computer can only stop one. By preventing the corner from being taken, the strategy is blocked. 

{% highlight javascript %}
function strategyCornerDefense() {
  if (val(0,1)==player && val(1,0)==player && val(0,0)=='') return [0,0];
  if (val(0,1)==player && val(1,2)==player && val(0,2)=='') return [0,2];
  if (val(1,2)==player && val(2,1)==player && val(2,2)=='') return [2,2];
  if (val(2,1)==player && val(1,0)==player && val(2,0)=='') return [2,0];
  return false;
}
{% endhighlight %}

### Play Tic Tac Toe

<a href="/projects/tic-tac-toe/index.html">Play the final version of the game</a>


### Final Source Code

<script src="https://gist.github.com/wiseley/9458565.js"></script>


