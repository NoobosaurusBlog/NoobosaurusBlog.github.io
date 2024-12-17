---
date: 2024-12-15
title: "Webpage Infos Extractor"
tags: ["tools", "script"]
---
When you need to quickly understand the structure of a webpage, a lightweight tool can save the day. **Webpage Infos Extractor** is just that: a simple JavaScript bookmarklet that extracts useful information like forms, links, images, and word count from any webpage. No extensions or extra software required—just a single bookmark to get key insights instantly.

## Why Build This?

Sometimes, the simplest tools are the most convenient. I needed a way to peek under the hood of webpages during quick tests or casual research without opening dev tools every time. So, I threw together this bookmarklet to make data analysis fast and portable. It’s not groundbreaking, but it gets the job done without any fuss.

## What Does It Do?

Once activated, the bookmarklet scans the current webpage and extracts:

- **Forms**: Shows details like form actions, methods, and input elements.
    
- **Links**: Lists all hyperlinks found on the page.
    
- **Images**: Displays all images in an easy-to-view layout.
    
- **Word Count**: Calculates the total number of words in the page’s text content.
    

The results are neatly presented in a new browser window with clean formatting, so you can analyze everything at a glance.

## Installation

Setting it up is simple. Here’s how:

1. Open your web browser and create a new bookmark.
    
2. Edit the bookmark’s URL field and paste the following JavaScript code:
    
    ```
    javascript:(function(){var forms=document.getElementsByTagName('form');var links=document.getElementsByTagName('a');var images=document.getElementsByTagName('img');var bodyText=document.body.innerText;var wordCount=bodyText.split(/\s+/).filter(function(word){return word.length>0;}).length;var newWindow=window.open('','','width=800,height=600');newWindow.document.write('<html><head><title>Extracted Data</title>');newWindow.document.write('<style>body{font-family:Arial,sans-serif}table{width:100%;border-collapse:collapse;margin-bottom:20px}th,td{border:1px solid #ddd;padding:8px;text-align:left}th{background-color:#f2f2f2}tr:nth-child(even){background-color:#f9f9f9}h2{background-color:#4CAF50;color:white;padding:10px}</style></head><body>');newWindow.document.write('<h2>Forms:</h2>');for(var i=0;i<forms.length;i++){var form=forms[i];newWindow.document.write('<table><tr><th colspan="3">Form '+(i+1)+'</th></tr>');newWindow.document.write('<tr><td>Action</td><td colspan="2">'+(form.action||'N/A')+'</td></tr>');newWindow.document.write('<tr><td>Method</td><td colspan="2">'+(form.method||'get')+'</td></tr>');newWindow.document.write('<tr><th>Name</th><th>Type</th><th>Value</th></tr>');for(var j=0;j<form.elements.length;j++){var element=form.elements[j];var value=element.value||'N/A';if(element.type==='checkbox'||element.type==='radio'){value=element.checked?'on':'off'}newWindow.document.write('<tr><td>'+(element.name||'N/A')+'</td><td>'+(element.type||'N/A')+'</td><td>'+value+'</td></tr>')}newWindow.document.write('</table>')}newWindow.document.write('<h2>Links:</h2><table><tr><th>Link</th></tr>');for(var i=0;i<links.length;i++){newWindow.document.write('<tr><td><a href="'+links[i].href+'" target="_blank">'+links[i].href+'</a></td></tr>')}newWindow.document.write('</table>');newWindow.document.write('<h2>Images:</h2>');for(var i=0;i<images.length;i++){newWindow.document.write('<img src="'+images[i].src+'" style="max-width:100%;display:block;margin-bottom:10px;">')}newWindow.document.write('<h2>Word Count:</h2><p>'+wordCount+' words</p>');newWindow.document.write('</body></html>');newWindow.document.close();})();
    ```
    
3. Save the bookmark.
    

That’s it! You now have a bookmarklet ready to extract webpage info.

## How to Use

1. Navigate to the webpage you want to analyze.
    
2. Click on the saved bookmarklet.
    
3. A new window will pop up with the following details:
    
    - **Forms**: Lists actions, methods, and input fields.
        
    - **Links**: Displays all hyperlinks found on the page.
        
    - **Images**: Previews all images on the page.
        
    - **Word Count**: Shows the total word count of the page’s text content.
        

## Why Use It?

This tool is perfect for:

- **Web Developers**: Debugging forms, analyzing links, or reviewing images for optimization.
    
- **Content Creators**: Counting words or inspecting embedded media.
    
- **Researchers**: Extracting links or analyzing page structures quickly.
    

It’s not trying to replace full-fledged tools like browser dev tools, but it’s great for quick insights without digging into a complex interface.

## Limitations

This bookmarklet is lightweight and portable, but it’s not flawless. Here are a few things to keep in mind:

1. **Browser Compatibility**: It works on most modern browsers but may struggle with certain page structures or dynamic content.
    
2. **Static Analysis**: It doesn’t execute JavaScript-heavy elements, so it’s best suited for simpler pages.
    
3. **Basic Formatting**: The output is clean but not customizable.
    

## Final Thoughts

The Webpage Infos Extractor isn’t revolutionary, but it’s incredibly handy. Whether you’re troubleshooting a webpage or casually analyzing content, this bookmarklet gives you the essentials at a click. Simple, portable, and effective (sometimes), that’s all you need. If you think of ways to enhance it, feel free to tweak the code and make it your own!
