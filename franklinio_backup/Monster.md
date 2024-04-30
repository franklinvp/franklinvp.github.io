---
layout: page
navbar-links:
---

<html>
  <head>
    <meta charset="utf-8"/>
    <title>Hairy Monster</title>
    <script>
      
      function NormSInv(p) {
      var a1 = -39.6968302866538, a2 = 220.946098424521, a3 = -275.928510446969;
      var a4 = 138.357751867269, a5 = -30.6647980661472, a6 = 2.50662827745924;
      var b1 = -54.4760987982241, b2 = 161.585836858041, b3 = -155.698979859887;
      var b4 = 66.8013118877197, b5 = -13.2806815528857, c1 = -7.78489400243029E-03;
      var c2 = -0.322396458041136, c3 = -2.40075827716184, c4 = -2.54973253934373;
      var c5 = 4.37466414146497, c6 = 2.93816398269878, d1 = 7.78469570904146E-03;
      var d2 = 0.32246712907004, d3 = 2.445134137143, d4 = 3.75440866190742;
      var p_low = 0.02425, p_high = 1 - p_low;
      var q, r;
      var retVal;

      if ((p < 0) || (p > 1))
        {
            alert("NormSInv: Argument out of range.");
            retVal = 0;
        }
        else if (p < p_low)
        {
            q = Math.sqrt(-2 * Math.log(p));
            retVal = (((((c1 * q + c2) * q + c3) * q + c4) * q + c5) * q + c6) / ((((d1 * q + d2) * q + d3) * q + d4) * q + 1);
        }
        else if (p <= p_high)
      {
      q = p - 0.5;
      r = q * q;
      retVal = (((((a1 * r + a2) * r + a3) * r + a4) * r + a5) * r + a6) * q / (((((b1 * r + b2) * r + b3) * r + b4) * r + b5) * r + 1);
      }
      else
      {
      q = Math.sqrt(-2 * Math.log(1 - p));
      retVal = -(((((c1 * q + c2) * q + c3) * q + c4) * q + c5) * q + c6) / ((((d1 * q + d2) * q + d3) * q + d4) * q + 1);
      }

      return retVal;
      }

      function randomPath(){
      var x = 500;
      var y = 500;
      var xstep = 0;
      var ystep = 0;
      var path = '500,500';
      for (var k = 0; k < 300 ; k++) {
              path += ' ';
              path += (x).toString();
              path += ',';
              path += (y).toString();
              xstep = NormSInv(Math.random());
              ystep = NormSInv(Math.random());
              xstep *= 10;
              ystep *= 10;
              x += Math.trunc(xstep);
              y += Math.trunc(ystep);
            };
            return path;
      };
      
      function zero(){
        var path = '500,400';
        for (var k = 0; k < 300; k++){
          path += ' 500,400';
        };
        return path;
      };
            
      var namespace = 'http://www.w3.org/2000/svg';
      window.onload = function() {        
        var figure = document.createElementNS(namespace,'svg');
        figure.id = 'brownian-figure';
        figure.setAttribute('height', '100%');
        figure.setAttribute('width', '100%');
      
        var pathArray = [];
        var animationArray = [];
        var collapseAnimationArray = [];
        
        for (var i = 0; i < 100; i++){
        pathArray[i] = document.createElementNS(namespace,'polyline');
        pathArray[i].id = "hair" + (i).toString();
        var path = randomPath();
        pathArray[i].setAttribute('points', path);
        pathArray[i].setAttribute('style', 'fill:none;stroke:rgba(0,0,0,1);stroke-width:1');
        pathArray[i].setAttribute('onclick', 'moveHair("animation' + (i).toString() + '")');
        figure.appendChild(pathArray[i]);
        
        animationArray[i] = document.createElementNS(namespace, 'animate');
        animationArray[i].setAttribute('id', 'animation' + (i).toString());
        animationArray[i].setAttribute('attributeName', 'points');
        animationArray[i].setAttribute('begin', 'animation' + ((i+1) % 100).toString() + '.begin + 0.1s');
        animationArray[i].setAttribute('dur', '2s');
        animationArray[i].setAttribute('repeatCount', 'indefinite');
        animationArray[i].setAttribute('from', pathArray[i].getAttribute('points'));
        animationArray[i].setAttribute('values', pathArray[i].getAttribute('points') + '; ' + randomPath() + '; ' + pathArray[i].getAttribute('points'));
        animationArray[i].setAttribute('to', pathArray[i].getAttribute('points'));
        pathArray[i].appendChild(animationArray[i]);
        
        collapseAnimationArray[i] = document.createElementNS(namespace, 'animate');
        collapseAnimationArray[i].setAttribute('id', 'collapse' + (i).toString());
        collapseAnimationArray[i].setAttribute('attributeName', 'points');
        collapseAnimationArray[i].setAttribute('begin', 'indefinite');
        collapseAnimationArray[i].setAttribute('dur', '3s');
        collapseAnimationArray[i].setAttribute('from', pathArray[i].getAttribute('points'));
        collapseAnimationArray[i].setAttribute('to', zero());
        collapseAnimationArray[i].setAttribute('fill', 'freeze');
        pathArray[i].appendChild(collapseAnimationArray[i]);
        };
      
        var divfigure = document.createElement('div');
        divfigure.id = 'divfigure';
        //divfigure.setAttribute('onclick', 'moveHair()');
        divfigure.style = 'margin:0pt;padding:0pt;border:0pt none;background-color:rgba(240,240,240,0.66);width:99vw;height:99vh;';
        divfigure.appendChild(figure);
          
        //var content = document.getElementByName('footer');
        document.body.insertBefore(divfigure, document.body.firstChild);
      };
      
      var hairs_moving = 0;
      function moveHair(the_id){
        var animation = document.getElementById(the_id);
        animation.beginElement()
        hairs_moving += 1;
        //var message = document.createElement('p');
        //message.id = 'alertmessage';
        //var body = document.getElementById('content-container');
        //body.appendChild(message);
        
        if (hairs_moving > 5) {
          for (var t = 0; t < 100; t++){
          var hair = document.getElementById("hair" + (t).toString())
          var shake = document.getElementById('animation' + (t).toString());
          hair.removeChild(shake);
          var collapse = document.getElementById('collapse' + (t).toString());
          collapse.beginElement();
          };
          //var message = document.getElementById('alertmessage');
          //message.innerHTML = 'You&#39;ve killed the poor hairy monster!<br/> Now we need to give you a fresh one!';
          //message.style = 'font-size:20pt';
          window.setTimeout(partB,5000);
        } else {
          //var message = document.getElementById('alertmessage');
          //message.innerHTML = 'The monster&#39;s awake and needs computing power!<br/>Quick! Click it into surrender!';
          //message.style = 'font-size:15pt';
          };
      };
      
  function partB(){
  location.reload();
  }
    </script>
  </head>
  <body>
  </body>
</html>
