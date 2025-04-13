# Tracking Projects in Obsidian with ProgressBar


[![Tracking Projects in Obsidian](https://i.imgur.com/3YQmlli.png)](https://www.youtube.com/watch?v=3S5GWqcOCRU)
Click en la imagen para ver el video

```dataviewjs
function projectTracker(dv, query) {
    let searchPagePaths = dv.pages(query).file.path
    
    for(let i=0; i < searchPagePaths.length; i++){
        if(dv.page(searchPagePaths[i]).Total){
                    let title = dv.page(searchPagePaths[i]).title;
                    console
                    let total = dv.page(searchPagePaths[i]).Total;
                    let status = ((dv.page(searchPagePaths[i]).Completed / dv.page(searchPagePaths[i]).Total) * 100).toFixed();
                    const progress = "![pb|500](https://progress-bar.dev/" + status + "/?scale=" + "100" + "&title=" + title + "&width=400)"; //you could set any width if you need
                    dv.paragraph(progress);
                    dv.paragraph("<br>"); //use this if you have many projects to track.
        }
    }
} 

projectTracker(
    dv,
    "#projects" //change tag if you need
)
```

**NOTA:** Aún no se tiene realizado el video de estos cambios pero cuando se modifique se tendra el mismo en el canal de YouTube puedes seguir el video que se encuentra aqui para la configuración que aun se mantiene. Si se desea cambiar algo adicional en la forma de presentacion de las barras de progreso se debe de modificar el CSS en el dataviewjs de ambos escenarios presentados. 


Debido a que el sitio web progress-bar.dev dejo de estar disponible se tiene la siguiente modificación para trabajar unicamente con CSS se debe de modificar solo el tag respectivo a trackear. ademas que en caso de que no este ninguna tarea solo se muestra el nombre de la nota respectivamente.  


![](https://i.imgur.com/XYIjsyx.png)

```dataviewjs
function projectTracker(dv, query) {
    let searchPages = dv.pages(query);

    for (let page of searchPages) {
        if (page.Total) {
            let title = page.Title || page.file.name;
            let total = page.Total;
            let completed = page.Completed || 0;
            let percent = Math.round((completed / total) * 100);

            let barColor = percent < 50 ? "#d5763f" : "#4caf50"; 
            let backgroundColor = "#444"; 
            let progressBar = `<div style="background-color:${backgroundColor}; border-radius:10px; overflow:hidden; display:flex; height:30px; margin-bottom:16px;"> ${
                        percent === 0
                        ? `<div style="width:20%; padding-left:10px; display:flex; align-items:center; color:white; font-weight:bold;">${title}</div>` :
                         `<div style="background-color:${barColor}; width:${percent}%; color:white; display:flex; justify-content:space-between; align-items:center; padding:0 10px; font-weight:bold;"> <span>${title}</span> <span>${percent}%</span> </div>` } <div style="flex-grow:1;"></div> </div> `;

            dv.paragraph(progressBar);
        }
    }
}

projectTracker(
    dv,
    "#Proyectos" // Tag que se quiere monitorear. 
);

```

Esta modificación permite hacer el trackeo de más de un proyecto por la barra de progreso que se configura  al finalizar el script de **dataviewjs** los tags a monitorear. 

![](https://i.imgur.com/6AuLpXK.png)


```dataviewjs
function projectTracker(dv, tags = []) {
    for (let tag of tags) {
        let searchPages = dv.pages(tag);
        for (let page of searchPages) {
            if (page.Total) {
                let title = page.Title || page.file.name;
                let total = page.Total;
                let completed = page.Completed || 0;
                let percent = Math.round((completed / total) * 100);
                let barColor = percent < 50 ? "#d5763f" : "#4caf50";
                let backgroundColor = "#444";
                let progressBar = `<div style="background-color:${backgroundColor}; border-radius:10px; overflow:hidden; display:flex; height:30px; margin-bottom:16px;"> ${ percent === 0 ? `<div style="width:0%; padding-left:10px; display:flex; align-items:center; color:white; font-weight:bold;">${title}</div>` : `<div style="background-color:${barColor}; width:${percent}%; color:white; display:flex; justify-content:space-between; align-items:center; padding:0 10px; font-size:10px; font-weight:bold;"> <span>${title}</span> <span>${percent}%</span> </div>` } <div style="flex-grow:1;"> </div> </div>`;

                dv.paragraph(progressBar);
            }
        }
    }
}
projectTracker(dv, ["#Proyectos", "#Lectura", "#Curso"]); // Los tags de proyectos que deseas ver el progreso.
```



[![Suscribete al Boletin](https://i.imgur.com/rKxYGJv.png)](https://micerebroerrante.substack.com/)




[Original Post](https://forum.obsidian.md/t/project-tracking-metaedit-dataview-and-kanban/19343)
