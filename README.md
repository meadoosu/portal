# portal
 A web browser app that essentially rotates photos you add, and plays spotify. Oh yeah, you self host it! how cool is that? 

 how to set up:

 1. set up config.json (failure to do so will make your portal self destruct and turn evil)
    1a. make a spotify developer account with your normal spotify account, then after that: it'll prompt you to make a app, follow their instructions. once you have your app, grab your client ID and paste it into the config.json, go back to the spotify developer portal and paste in the URL you will be hosting this on, both the uris you input in config.json and the developer app NEEDS to be the same, or else you wouldnt be able to login to spotify.
    2a. add your image paths, again if you have alot of images, wouldnt recommend this app. start off by going to your images folder and noting the names of your files, then paste them in. this step requires a little of json knowledge. 
    3a. set up your location: go back to config.json and insert A. your city with state (example: Dallas, TX or Los Angeles, CA) 
