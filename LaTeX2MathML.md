---
layout: page
navbar-links:
---

<html>
  <head>
    <meta charset="utf-8"/>
    <title>LaTeX to MathML</title>
    <script type="text/x-mathjax-config">
      MathJax.Hub.Config({
      extensions: ["tex2jax.js"],
      extensions: ["toMathML.js"],
      jax: ["input/TeX", "output/HTML-CSS"],
      tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      displayMath: [ ['$$','$$'], ["\\[","\\]"] ],
      processEscapes: true
      },
      "HTML-CSS": { availableFonts: ["TeX"]}
      });
    </script>
    <script type="text/javascript"  
            src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.5/MathJax.js?config=TeX-MML-AM_CHTML">
    </script>
    <script>
      function copyToClipboard() {
        var range = document.createRange();
        range.selectNode(document.getElementById("MathMLRaw"));
        var text = range.toString().trim();
        var dummy = document.createElement("textarea");
        document.body.appendChild(dummy);
        dummy.value = text;
        window.getSelection().removeAllRanges(); // clear current selection
        dummy.select();
        document.execCommand("copy");
        document.body.removeChild(dummy);
        /*window.getSelection().removeAllRanges(); // clear current selection*/
        /*window.getSelection().addRange(range); // to select text*/
        /*document.execCommand("copy");*/
        window.getSelection().removeAllRanges();// to deselect
        var message = document.getElementById("CopiedMessage");
        message.className="copiedMessageVisible";
        window.setTimeout(function(){message.className="copiedMessage";}, 500);
      } 

      function switchTip(theid,thesize) {
        var image = document.getElementById(theid);
        if (image.className == 'tooltiptext') {
          image.className = thesize;
        } else {
          image.className = 'tooltiptext';
        }
      }

      function saveAllToLocalStorage(){
        localStorage.setItem('latex_input', document.getElementById('LaTeXInputBox').value);
		var mml = document.getElementById('MathMLRaw').innerHTML;
		mml = mml.replace(/<m:mrow class="MJX-TeXAtom-ORD">/g, "<m:mrow>");
		mml = mml.replace(/<mrow class="MJX-TeXAtom-ORD">/g, "<mrow>");
        localStorage.setItem('mml_output', mml);
        localStorage.setItem('math_output', document.getElementById('MathOutput').innerHTML);
        localStorage.setItem('displayinlinechecked', document.getElementById('display-inline').checked);
        localStorage.setItem('itagschecked', document.getElementById('itags').checked);
        localStorage.setItem('compactchecked', document.getElementById('NoBreakLines').checked);
      }

      function recalling(){
        var checkboxids = ['display-inline', 'itags', 'NoBreakLines'];
        var storagechecked = ['displayinlinechecked', 'itagschecked', 'compactchecked'];
        var trasformation = [toggleInlineDisplay, toggleitags, toggleBreakLines];
        /*If LaTeX is saved, then recall everything, otherwise start fresh*/
        var latex = localStorage.getItem('latex_input');
        if (latex === null || latex == '') {
          var default_latex_input = '\\color{gray}{\\text{Input LaTeX here}\\rightarrow\\LaTeX=mc^2}';
          document.getElementById('LaTeXInputBox').value = '';
          for (i = 0; i < 3; i++) {
            document.getElementById(checkboxids[i]).checked = Boolean(i == 1);
          }
          saveAllToLocalStorage();
        } else {
          document.getElementById('LaTeXInputBox').value = latex;
          document.getElementById('MathMLRaw').innerHTML = localStorage.getItem('mml_output');
          var checkbox, checked, i;
          for (i = 0; i < 3; i++) {
            checkbox = document.getElementById(checkboxids[i]);
            checked = localStorage.getItem(storagechecked[i]);
            if (checked === null) {
              checkbox.checked = Boolean(i == 1);
              localStorage.setItem(storagechecked[i], Boolean(i == 1));
            } else {
              checkbox.checked = Boolean(checked == 'true');
            }
          }
        }
        document.getElementById('LaTeXInputBox').focus();
      }

      function toMathML(jax, callback) {
        var mml;
        try {
            mml = jax.root.toMathML("");
			mml = mml.replace(/<(.*) class=".*"(.*)>/g, "<$1$2>");
        } catch(err) {
            if (!err.restart) {throw err} // an actual error
            return MathJax.Callback.After([toMathML, jax, callback], err.restart);
        }
        MathJax.Callback(callback)(mml);
      }

      function toggleInlineDisplay(element) {
        var mml = document.getElementById('MathMLRaw').innerHTML;
        var ibmTags = document.getElementById('itags').checked;
        if (element.checked) {
          mml = mml.replace("<equation-inline>", "<equation-display>");
          mml = mml.replace("</equation-inline>", "</equation-display>");
          /* 
          if (ibmTags) {
            mml = mml.replace("<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">",
                              "<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">");
          } else {
            mml = mml.replace("<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">",
                              "<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">");
          }*/
        } else {
          mml = mml.replace("<equation-display>", "<equation-inline>");
          mml = mml.replace("</equation-display>", "</equation-inline>");
          if (ibmTags) {
            mml = mml.replace("<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">",
                              "<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">");
          } else {
            mml = mml.replace("<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">",
                              "<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">");
          }
        }
        localStorage.setItem('mml_output', mml);
        document.getElementById('MathMLRaw').innerHTML = mml;
        localStorage.setItem('displayinlinechecked', element.checked);
      }

      function toggleitags(element) {
        var mml = localStorage.getItem('mml_output');
        if (element.checked) {
          mml = mml.replace(/<m/g, "<m:m");
          mml = mml.replace(/<\/m/g, "<\/m:m");
          mml = mml.replace("xmlns=", "xmlns:m=");
          mml = mml.replace("<m:mathml>", "<mathml>");
          mml = mml.replace("</m:mathml>", "</mathml>");
        } else {
          mml = mml.replace(/<m:m/g, "<m");
          mml = mml.replace(/<\/m:m/g, "<\/m");
          mml = mml.replace("xmlns:m=", "xmlns=");
        }
        document.getElementById('MathMLRaw').innerHTML = mml;
        localStorage.setItem('mml_output', mml);
        localStorage.setItem('itagschecked', element.checked);
      }

      function toggleBreakLines(element) {
        var mml = document.getElementById('MathMLRaw').innerHTML;
        if (element.checked) {
          mml = mml.replace(/>\s*</g, "><");
        } else {
          UpdateMath(document.getElementById('LaTeXInputBox').value);
          mml = document.getElementById('MathMLRaw').innerHTML;
        }
        document.getElementById('MathMLRaw').innerHTML = mml;
        localStorage.setItem('mml_output', mml);
        localStorage.setItem('compactchecked', element.checked);
      }
    </script>
    <script>
      var math = null; // the element jax for the math output.
      //
      //  Get the element jax when MathJax has produced it.
      //
      MathJax.Hub.queue.Push(function () {
        math = MathJax.Hub.getAllJax("MathOutput")[0];
      });
      //
      //  The onchange event handler that typesets the
      //  math entered by the user
      //
      window.UpdateMath = function (TeX) {
        var TeXtoTransform = TeX;
        MathJax.Hub.queue.Push(["Text", math, TeXtoTransform]);
        toMathML(math, function (mml) {
          var ibmTags = document.getElementById('itags').checked;
          if (ibmTags) {   
            mml = mml.replace(/<m/g, "<m:m");
            mml = mml.replace(/<\/m/g, "</m:m");
            mml = mml.replace("xmlns", "xmlns:m");
          }
          var eqtypeopen;
          var eqtypeclose;
          var checkboxval = document.getElementById('display-inline').checked;
          if (checkboxval) {
            eqtypeopen = "<equation-display>";
            eqtypeclose = "</equation-display>";
          } else {
            eqtypeopen = "<equation-inline>";
            eqtypeclose = "</equation-inline>";
            if (ibmTags) {
              mml = mml.replace("<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">", 
                                "<m:math xmlns:m=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">");
            } else {
              mml = mml.replace("<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\" display=\"block\">",
                                "<math xmlns=\"http:\/\/www\.w3\.org\/1998\/Math\/MathML\">");
            }
          }
          mml = eqtypeopen + "\n<mathml>\n" + mml + "\n</mathml>\n" + eqtypeclose;
          if (document.getElementById('NoBreakLines').checked) {
            mml = mml.replace(/>\s*</g, "><");
          }
          if (TeX != '') {
            document.getElementById('MathMLRaw').innerHTML = mml;
          } else {
            document.getElementById('MathMLRaw').innerHTML = ''; 
          }
          saveAllToLocalStorage();
        });
      };

      function pressdown(item) {
        item.classList.add('no-hover');
      }

      function pullup(item) {
      item.classList.remove('no-hover');
      }
    </script>
    <style>
       .copybutton {
         background-color:rgba(250, 250, 250, 1);
         border-radius: 4pt;
         padding: 5pt;
       }

       .copybutton:not(.no-hover):hover {
         background-color:rgb(255, 255, 255);
         box-shadow: 2px 2px 8px rgba(50, 50, 50, 1);
       }

       /* Tooltip container */
       .tooltip {
         visibility: visible;
         display: inline-block;

         padding:5pt;
         display:block;
         background-color:rgba(250, 250, 250, 1);
         border-radius:4pt;
         -webkit-touch-callout: none;
         -webkit-user-select: none;
         -khtml-user-select: none;
         -moz-user-select: none;
         -ms-user-select: none;
         -o-user-select: none;
         user-select: none;
       }

       .tooltip:not(.no-hover):hover {
         background-color:rgb(255, 255, 255);
         box-shadow: 2px 2px 8px rgba(50, 50, 50, 1);
       }

       /* Tooltip text */
       .tooltip .tooltiptext {
         visibility: hidden;
         background-color: #555;
         color: #fff;
         text-align: center;
         padding: 5px 0;
         border-radius: 6px;

         /* Position the tooltip text */
         z-index: 2;
         left: 50vw;
         height:95vh;
         margin-left: -60px;

         /* Fade in tooltip */
         opacity: 0;
         transition: opacity 0.3s;
       }

       /* Tooltip arrow */
       .tooltip .tooltiptext::after {
       content: "";
       position: absolute;
       left: 50%;
       margin-left: -5px;
       border-width: 5px;
       border-style: solid;
       border-color: #555 transparent transparent transparent;
     }

     /* Show the tooltip text when you mouse over the tooltip container */
     .tooltip .showtip {
       visibility: visible;
       background-color: #555;
       color: #fff;
       text-align: center;
       padding: 5px 0;
       border-radius: 6px;

       /* Position the tooltip text */
       position: fixed;
       z-index: 3;
       left: 50vw;
       height:95vh;
       margin-left: -60px;
     }

     .tooltip .bigtip {
       visibility: visible;
       background-color: #555;
       color: #fff;
       text-align: center;
       padding: 5px 0;
       border-radius: 6px;

       /* Position the tooltip text */
       left: 5vw;
       width: 1700px;
       height: 2200px;
       z-index: 3;
       margin-left: -60px;
     }

      .copiedMessage {
        opacity: 0;
        z-index: 10;
        padding: 5pt;
        border-radius:4pt;    
      }

      .copiedMessageVisible {
        opacity: 1;
        z-index: 10;
        padding: 5pt;
        border-radius:4pt;
        background-color:rgba(255,255,224, 0.9);
        box-shadow: 0px 0px 8px rgba(50, 50, 50, 1);
      } 

      .copiedMessageFade {
        opacity 0;
      }
    </style>
  </head>
  <body id="uniqueidentifier" onload="recalling()" style="overflow-x:hidden;">
    <div cols="35" rows="2"
         style="resize: none;
                height=3em;
                background-color: rgba(250,250,250,0);
                border:none;">
       <input type="checkbox" id="display-inline" onchange = "toggleInlineDisplay(this)"/>Displayed equation
       <input type="checkbox" id="itags" checked="true" onchange = "toggleitags(this)"/>NS tags
       <input type="checkbox" id="NoBreakLines" onchange = "toggleBreakLines(this)"/>Compact
    </div>
    <!--
    <div class="tooltip" 
         onmousedown="pressdown(this)"
         onmouseup="pullup(this)"
         onclick="switchTip('img1', 'showtip')"
         ondblclick="switchTip('img1', 'bigtip')">Cheat sheet $1$
      <img id="img1" class="tooltiptext" src="assets/img/CheatSheet1.png" alt="Cheatsheet 1" 
           style="box-shadow: 2px 2px 8px rgba(100, 100, 100, 1);
                  border-radius: 4pt;">
    </div>
    <div class="tooltip" 
         onmousedown="pressdown(this)"
         onmouseup="pullup(this)"
         onclick="switchTip('img2', 'showtip')"
         ondblclick="switchTip('img2', 'bigtip')">Cheat sheet $2$
      <img id="img2" class="tooltiptext" src="assets/img/CheatSheet2.png" alt="Cheatsheet 2" 
           style="box-shadow: 2px 2px 8px rgba(100, 100, 100, 1);
                  border-radius: 4pt;">
    </div>
    -->
    <div id="CopyToClipboard"
         class="copybutton"
         style="top: 3em;
                margin-top: 1em;
                z-index: 10;
                -webkit-touch-callout: none;
                -webkit-user-select: none;
                -khtml-user-select: none;
                -moz-user-select: none;
                -ms-user-select: none;
                -o-user-select: none;
                user-select: none;
                background-color: rgba(255, 255, 255, 1);
                border-radius: 4pt;"
         onmousedown="pressdown(this)"
         onmouseup="pullup(this)"
         onclick="copyToClipboard()">Copy MathML</div>
    <div id="CopiedMessage"
         class="copiedMessage"
         style="position:absolute; top: calc(10em - 1pt); left:10em; z-index:10">MathML Copied</div>
    <div style="margin-top:1em; top:6em;">
      <textarea id="LaTeXInputBox" cols="70" rows="15" oninput="UpdateMath(this.value)" 
                style="float:left;
                       top: 7em;
                       width: 50%;
                       min-height: 22.5em;
                       resize: none;
                       background-color: rgba(250,250,250,1);
                       border: none;"
                placeholder="\text{Input LaTeX here}\rightarrow\LaTeX=mc^2"></textarea>
      <div style="float: right;
                  top: 7em;
                  width: 46%;
                  min-height: 22.5em;
                  max-height: 22.5em;
                  resize: none;
                  overflow-x: auto;
                  overflow-y: auto;
                  padding: 1em;
                  padding-left: 2em;
                  padding-right: 2em;
                  display: block;
                  background-color: rgba(250, 250, 250, 1);
                  box-shadow: 2px 2px 8px rgba(190, 190, 190, 1) inset;
                  border-radius: 4pt;
                  border: none;">
          <xmp id="MathMLRaw"></xmp>
      </div>    
    </div>
    <div id="MathOutput" class="mathoutputclass"
         style="max-width: 90vw;
                min-width: 100%;
                float: left;
                margin-top: 1em;
                top: 50em;
                overflow: auto;
                background-color: rgba(255,255,255,0.9);
                -ms-transform: translateY(-50%, -50%);
                transform: translateY(-50%, -50%);
                z-index: 2;
                min-width: calc(40vw - 4em);
                min-height: calc(40vh - 2em);
                box-shadow: 0px 0px 8px rgba(100, 100, 100, 1);
                padding: 1em;
                padding-left: 2em;
                padding-right: 2em;">$${}$$</div>
  </body>
</html>
