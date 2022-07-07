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

[Original Post](https://forum.obsidian.md/t/project-tracking-metaedit-dataview-and-kanban/19343)
