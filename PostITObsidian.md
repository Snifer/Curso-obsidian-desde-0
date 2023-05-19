Css extraido del tema Shimmerin Focus, permite  crear post it en nuestras notas en Obsidian a traves de un callout puedes ver el video completo del uso en el siguiente enlace. 

**https://youtu.be/d5NVPdq9wjw**



```CSS
.callout[data-callout*=sidenote] {
	--callout-icon: lightbulb;
	--callout-color:  85, 255, 51;
	font-size: 90%;
	line-height: 1.3em;
	max-width: calc(var(--file-line-width) * var(--sidenote-callout-width) * .01);
	margin: 4px 0 4px 7px;
	float: right
}

.sidenote-callout-outdent .callout[data-callout$=sidenote] {
	margin-right: -30px
}

.callout[data-callout*=sidenote] .callout-title {
	padding-top: 1px;
	padding-bottom: 1px
}

body .callout {
	clear: right
}
```
