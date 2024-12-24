onst fileInput = document.querySelector(".file-input"), 

filterOptions = document.querySelectorAll(".filter button"), 

filterName = document.querySelector(".filter-info .name"), 

filterValue = document.querySelector(".filter-info .value"), 

filterSlider = document.querySelector(".slider input"), 

rotateOptions = document.querySelectorAll(".rotate button"), 

previewImg = document.querySelector(".preview-img img"), 

resetFilterBtn = document.querySelector(".reset-filter"), 


//<!--chooseImgBtn = document.querySelector(".choose-img"),--> 

saveImgBtn = document.querySelector(".save-img"); 

 

let brightness = "100", saturation = "100", inversion = "0", grayscale = "0", blur = "0", contrast = "100", opacity = "100";; 

let rotate = 0, flipHorizontal = 1, flipVertical = 1; 

 

const loadImage = () => { 

    let file = fileInput.files[0]; 

    if(!file) return; 

    previewImg.src = URL.createObjectURL(file); 

    previewImg.addEventListener("load", () => { 

        resetFilterBtn.click(); 

        document.querySelector(".container").classList.remove("disable"); 

    }); 

} 

 

const applyFilter = () => { 

    previewImg.style.transform = rotate(${rotate}deg) scale(${flipHorizontal}, ${flipVertical}); 

    previewImg.style.filter = brightness(${brightness}%) saturate(${saturation}%) invert(${inversion}%) grayscale(${grayscale}%) blur(${blur}px) contrast(${contrast}%); 

 

    previewImg.style.opacity = opacity / 100; // Convert opacity to a value between 0 and 1 

} 

 

filterOptions.forEach(option => { 

    option.addEventListener("click", () => { 

        document.querySelector(".active").classList.remove("active"); 

        option.classList.add("active"); 

        filterName.innerText = option.innerText; 

 

        if(option.id === "brightness") { 

            filterSlider.max = "200"; 

            filterSlider.value = brightness; 

            filterValue.innerText = ${brightness}%; 

        } else if(option.id === "saturation") { 

            filterSlider.max = "200"; 

            filterSlider.value = saturation; 

            filterValue.innerText = ${saturation}%; 

        } else if(option.id === "inversion") { 

            filterSlider.max = "100"; 

            filterSlider.value = inversion; 

            filterValue.innerText = ${inversion}%; 

        } else if(option.id === "grayscale") { 

            filterSlider.max = "100"; 

            filterSlider.value = grayscale; 

            filterValue.innerText = ${grayscale}%; 

        } else if(option.id === "blur") { 

            filterSlider.max = "20"; // Set max value for blur 

            filterSlider.value = blur; 

            filterValue.innerText = ${blur}px; 

 

        } else if(option.id === "contrast") { 

            filterSlider.max = "200"; // Set max value for contrast 

            filterSlider.value = contrast; 

            filterValue.innerText = ${contrast}%; 

        } else if(option.id === "opacity") { 

            filterSlider.max = "100"; // Set max value for opacity 

            filterSlider.value = opacity; 

            filterValue.innerText = ${opacity}%; 

        } 

    }); 

}); 

 

const updateFilter = () => { 

    filterValue.innerText = ${filterSlider.value}${filterSlider.dataset.unit || ''}; 

    const selectedFilter = document.querySelector(".filter .active"); 

 

    if(selectedFilter.id === "brightness") { 

        brightness = filterSlider.value; 

    } else if(selectedFilter.id === "saturation") { 

        saturation = filterSlider.value; 

    } else if(selectedFilter.id === "inversion") { 

        inversion = filterSlider.value; 

    } else if(selectedFilter.id === "grayscale") { 

        grayscale = filterSlider.value; 

    } else if(selectedFilter.id === "blur") { 

        blur = filterSlider.value; 

    } else if(selectedFilter.id === "contrast") { 

        contrast = filterSlider.value; 

    } else if(selectedFilter.id === "opacity") { 

        opacity = filterSlider.value; 

    } 

    applyFilter(); 

} 

 

rotateOptions.forEach(option => { 

    option.addEventListener("click", () => { 

        if(option.id === "left") { 

            rotate -= 90; 

        } else if(option.id === "right") { 

            rotate += 90; 

        } else if(option.id === "horizontal") { 

            flipHorizontal = flipHorizontal === 1 ? -1 : 1; 

        } else { 

            flipVertical = flipVertical === 1 ? -1 : 1; 

        } 

        applyFilter(); 

    }); 

}); 

 

const resetFilter = () => { 

    brightness = "100"; saturation = "100"; inversion = "0"; grayscale = "0"; 

    rotate = 0; flipHorizontal = 1; flipVertical = 1; 

    filterOptions[0].click(); 

    applyFilter(); 

} 

 

const saveImage = () => { 

    const canvas = document.createElement("canvas"); 

    const ctx = canvas.getContext("2d"); 

    canvas.width = previewImg.naturalWidth; 

    canvas.height = previewImg.naturalHeight; 

     

    ctx.filter = brightness(${brightness}%) saturate(${saturation}%) invert(${inversion}%) grayscale(${grayscale}%); 

    ctx.translate(canvas.width / 2, canvas.height / 2); 

    if(rotate !== 0) { 

        ctx.rotate(rotate * Math.PI / 180); 

    } 

    ctx.scale(flipHorizontal, flipVertical); 

    ctx.drawImage(previewImg, -canvas.width / 2, -canvas.height / 2, canvas.width, canvas.height); 

     

    const link = document.createElement("a"); 

    link.download = "image.jpg"; 

    link.href = canvas.toDataURL(); 

    link.click(); 

} 

 

filterSlider.addEventListener("input", updateFilter); 

resetFilterBtn.addEventListener("click", resetFilter); 

saveImgBtn.addEventListener("click", saveImage); 

fileInput.addEventListener("change", loadImage); 

chooseImgBtn.addEventListener("click", () => fileInput.click());
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap'); 

 

* { 

    margin: 0; 

    padding: 0; 

    box-sizing: border-box; 

    font-family: 'Poppins', sans-serif; 

} 

 

:root { 

    /* Base font size */ 

    font-size: 10px; 

    /* Set neon color */ 

    --neon-border-color: rgb(104, 65, 183); 

} 

 

body { 

    display: flex; 

    padding: 10px; 

    min-height: 100vh; 

    align-items: center; 

    justify-content: center; 

    background: radial-gradient(circle, rgba(238, 174, 202, 1) 0%, rgba(2, 131, 153, 1) 0%, rgba(0, 45, 255, 1) 0%, rgba(132, 150, 212, 0.9906556372549019) 67%, rgba(0, 47, 227, 1) 100%, rgba(228, 217, 228, 1) 100%); 

} 

 

.container { 

    width: 850px; 

    padding: 30px 35px 35px; 

    background: skyblue; 

    border-radius: 10px; 

    box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1); 

    animation: flicker 1.5s infinite alternate; 

} 

 

.container::-moz-selection { 

    background-color: var(--neon-border-color); 

    color: var(--neon-text-color); 

} 

 

.container::selection { 

    background-color: var(--neon-border-color); 

    color: var(--neon-text-color); 

} 

 

.container:focus { 

    outline: none; 

} 

 

.container.disable .editor-panel, 

.container.disable .controls .reset-filter, 

.container.disable .controls .save-img { 

    opacity: 0.69; 

    pointer-events: none; 

} 

 

.container h2 { 

    margin-top: -8px; 

    font-size: 22px; 

    font-weight: 500; 

    text-align: center; 

    font-style: normal; 

    color: #0f1315; 

} 

 

.container .wrapper { 

    display: flex; 

    margin: 20px 0; 

    min-height: 335px; 

} 

 

.wrapper .editor-panel { 

    padding: 15px 20px; 

    width: 280px; 

    border-radius: 5px; 

    border: 4px solid rgb(32, 106, 185); 

} 

 

.editor-panel .title { 

    display: block; 

    font-size: 16px; 

    margin-bottom: 12px; 

} 

 

.editor-panel .options, 

.controls { 

    display: flex; 

    flex-wrap: wrap; 

    justify-content: space-between; 

} 

 

.editor-panel button { 

    outline: none; 

    height: 40px; 

    font-size: 14px; 

    color: #6C757D; 

    background: #fff; 

    border-radius: 3px; 

    margin-bottom: 8px; 

    border: 1px solid #aaa; 

} 

 

.editor-panel .filter button { 

    width: calc(100% / 3 - 4px); /* Adjusted for 6 buttons */ 

} 

 

.editor-panel button:hover { 

    background: #f5f5f5; 

} 

 

.filter button.active { 

    color: #fff; 

    border-color: #5372F0; 

    background: #5372F0; 

} 

 

.filter .slider { 

    margin-top: 12px; 

} 

 

.filter .slider .filter-info { 

    display: flex; 

    color: #464646; 

    font-size: 14px; 

    justify-content: space-between; 

} 

 

.filter .slider input { 

    width: 100%; 

    height: 5px; 

    accent-color: #5372F0; 

} 

 

.editor-panel .rotate { 

    margin-top: 17px; 

} 

 

.editor-panel .rotate button { 

    display: flex; 

    align-items: center; 

    justify-content: center; 

    width: calc(100% / 4 - 3px); 

} 

 

.rotate .options button:nth-child(3), 

.rotate .options button:nth-child(4) { 

    font-size: 18px; 

} 

 

.rotate .options button:active { 

    color: #fff; 

    background: #5372F0; 

    border-color: #5372F0; 

} 

 

.wrapper .preview-img { 

    flex-grow: 1; 

    display: flex; 

    overflow: hidden; 

    margin-left: 20px; 

    border-radius: 5px; 

  align-items: center; 

  justify-content: center; 

} 

.preview-img img{ 

  max-width: 490px; 

  max-height: 335px; 

  width: 100%; 

  height: 100%; 

  object-fit: contain; 

} 

.controls button{ 

  padding: 11px 20px; 

  font-size: 14px; 

  border-radius: 3px; 

  outline: none; 

  color: #fff; 

  cursor: pointer; 

  background: none; 

  transition: all 0.3s ease; 

  text-transform: uppercase; 

} 

.controls .reset-filter{ 

  color: #6C757D; 

  border: 1px solid #6C757D; 

} 

.controls .reset-filter:hover{ 

  color: #fff; 

  background: #6C757D; 

} 

.controls .choose-img{ 

  background: #6C757D; 

  border: 1px solid #6C757D;           

} 

.controls .save-img{ 

  margin-left: 5px; 

  background: #5372F0; 

  border: 1px solid #5372F0; 

} 

 

@media screen and (max-width: 760px) { 

  .container{ 

    padding: 25px; 

  } 

  .container .wrapper{ 

    flex-wrap: wrap-reverse; 

  } 

  .wrapper .editor-panel{ 

    width: 100%; 

  } 

  .wrapper .preview-img{ 

    width: 100%; 

    margin: 0 0 15px; 

  } 

} 

 

@media screen and (max-width: 500px) { 

  .controls button{ 

    width: 100%; 

    margin-bottom: 10px; 

  } 

  .controls .row{ 

    width: 100%; 

  } 

  .controls .row .save-img{ 

    margin-left: 0px; 

  } 

}
<!DOCTYPE html> 

<html lang="en"> 

<head> 

    <meta charset="UTF-8"> 

    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 

    <title>Image Gallery</title> 

    <link rel="stylesheet" href="st.css"> <!-- Link to your existing CSS --> 

    <link rel="icon" href="logo1.png"> 

    <style> 

        body { 

            display: flex; 

            flex-direction: column; 

            align-items: center; 

            background: radial-gradient(circle, rgba(238,174,202,1) 0%, rgba(2,131,153,1) 0%, rgba(0,45,255,1) 0%, rgba(132,150,212,0.9906556372549019) 67%, rgba(0,47,227,1) 100%, rgba(228,217,228,1) 100%); 

            padding: 20px; 

        } 

 

        .gallery { 

            display: grid; 

            grid-template-columns: repeat(auto-fill, minmax(150px, 1fr)); 

            gap: 10px; 

            width: 100%; 

            max-width: 800px; 

        } 

 

        .gallery img { 

            width: 100%; 

            border-radius: 5px; 

            cursor: pointer; 

            transition: transform 0.2s; 

        } 

 

        .gallery img:hover { 

            transform: scale(1.05); 

        } 

 

        .back-button { 

            margin-top: 20px; 

            padding: 10px 20px; 

            background: #5372F0; 

            color: white; 

            border: none; 

            border-radius: 5px; 

            cursor: pointer; 

        } 

 

        .back-button:hover { 

            background: #475DAF; 

        } 

 

        .upload-button { 

            margin-top: 20px; 

            padding: 10px 20px; 

            background: #4CAF50; 

            color: white; 

            border: none; 

            border-radius: 5px; 

            cursor: pointer; 

        } 

 

        .upload-button:hover { 

            background: #45a049; 

        } 

 

        input[type="file"] { 

            display: none; /* Hide the default file input */ 

        } 

    </style> 

</head> 

<body> 

    <h2>Select an Image to Edit</h2> 

    <div class="gallery" id="gallery"></div> 

    <label class="upload-button" for="file-input">Upload Image</label> 

    <input type="file" id="file-input" accept="image/*" onchange="addImage(event)"> 

 

    <button class="back-button" onclick="goBack()">Back to Editor</button> 

 

    <script> 

   // Load images from local storage when the page loads 

window.onload = function() { 

    const images = JSON.parse(localStorage.getItem('images')) || []; 

    images.forEach(imageSrc => { 

        addImageToGallery(imageSrc); 

    }); 

}; 

 

function addImage(event) { 

    const file = event.target.files[0]; 

    if (file) { 

        const reader = new FileReader(); 

        reader.onload = function(e) { 

            const imageSrc = e.target.result; 

            addImageToGallery(imageSrc); 

            saveImageToLocalStorage(imageSrc); 

        }; 

        reader.readAsDataURL(file); 

    } 

} 

 

function addImageToGallery(imageSrc) { 

    const gallery = document.getElementById('gallery'); 

    const galleryItem = document.createElement('div'); 

    galleryItem.classList.add('gallery-item'); 

 

    const imgElement = document.createElement('img'); 

    imgElement.src = imageSrc; 

    imgElement.alt = 'Uploaded Image'; 

    imgElement.onclick = function() { 

        selectImage(imageSrc); 

    }; 

 

    const deleteButton = document.createElement('button'); 

deleteButton.classList.add('delete-button'); 

deleteButton.innerText = 'Delete'; 

deleteButton.style.background = 'green'; // Set background color to green 

deleteButton.style.color = 'white'; // Set text color to white 

deleteButton.onclick = function(event) { 

    event.stopPropagation(); // Prevent the image click event 

    deleteImage(imageSrc, galleryItem); 

}; 

 

    galleryItem.appendChild(imgElement); 

    galleryItem.appendChild(deleteButton); 

    gallery.appendChild(galleryItem); 

} 

 

function saveImageToLocalStorage(imageSrc) { 

    const images = JSON.parse(localStorage.getItem('images')) || []; 

    images.push(imageSrc); 

    localStorage.setItem('images', JSON.stringify(images)); 

} 

 

function deleteImage(imageSrc, galleryItem) { 

    // Remove the image from the gallery 

    galleryItem.remove(); 

 

    // Update local storage 

    const images = JSON.parse(localStorage.getItem('images')) || []; 

    const updatedImages = images.filter(src => src !== imageSrc); 

    localStorage.setItem('images', JSON.stringify(updatedImages)); 

} 

 

function selectImage(imageSrc) { 

    // Store the selected image in local storage 

    localStorage.setItem('selectedImage', imageSrc); 

    // Redirect to the image editor page 

    window.location.href = 'ind.html'; 

} 

 

function goBack() { 

    window.history.back(); 

} 

    </script> 

</body> 

</html>

            <div class="form-group"> 

                <label for="password">Password</label>  

                <input type="password" id="password" required> 

  …
 <!DOCTYPE html> 

<html lang="en"> 

<head> 

    <meta charset="utf-8"> 

    <title>Image Editor</title> 

    <link rel="icon" href="logo1.png"> 

    <link rel="stylesheet" href="st.css"> 

    <meta name="viewport" content="width=device-width, initial-scale=1.0"> 

    <link rel="stylesheet" href="https://unpkg.com/boxicons@2.1.2/css/boxicons.min.css"> 

    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.1.1/css/all.min.css"/> 

</head> 

<body> 

    <div class="container" id="editorContainer"> 

        <h2>Image Editor</h2> 

        <div class="wrapper"> 

            <div class="editor-panel"> 

                <div class="filter"> 

                    <label class="title">Filters</label> 

                    <div class="options"> 

                        <button id="brightness" class="active">Brightness</button> 

                        <button id="saturation">Saturation</button> 

                        <button id="inversion">Inversion</button> 

                        <button id="grayscale">Grayscale</button> 

                        <button id="blur">Blur</button> 

                        <button id="contrast">Contrast</button> 

                        <button id="opacity">Opacity</button> 

                    </div> 

                    <div class="slider"> 

                        <div class="filter-info"> 

                            <p class="name">Brightness</p> 

                            <p class="value">100%</p> 

                        </div> 

                        <input type="range" value="100" min="0" max="200"> 

                    </div> 

                </div> 

                <div class="rotate"> 

                    <label class="title">Rotate & Flip</label> 

                    <div class="options"> 

                        <button id="left"><i class="fa-solid fa-rotate-left"></i></button> 

                        <button id="right"><i class="fa-solid fa-rotate-right"></i></button> 

                        <button id="horizontal"><i class='bx bx-reflect-vertical'></i></button> 

                        <button id="vertical"><i class='bx bx-reflect-horizontal'></i></button> 

                    </div> 

                </div> 

            </div> 

            <div class="preview-img"> 

                <img src="logo3.jpeg" alt="Select Image To Proceed"> 

            </div> 

        </div> 

        <div class="controls"> 

            <button class="reset-filter">Reset Filters</button> 

            <div class="row"> 

                <button class="save-img">Save Image</button> 

                <button class="back-to-gallery" onclick="goToGallery()">Back to Gallery</button> 

            </div> 

        </div> 

    </div> 

 

    <script src="app.js"></script> 

    <script> 

        // Check if the user is logged in (for demonstration purposes) 

        const isLoggedIn = true; // Change this based on your authentication logic 

 

        if (!isLoggedIn) { 

            window.location.href = 'login.html'; // Redirect to login page if not logged in 

        } 

 

        // Load the selected image from local storage 

        window.onload = function() { 

            const selectedImage = localStorage.getItem('selectedImage'); 

            if (selectedImage) { 

                document.querySelector('.preview-img img').src = selectedImage; 

            } else { 

                // Optionally, you can handle the case where no image is selected 

                console.warn('No image selected. Please select an image from the gallery.'); 

            } 

        }; 

 

        // Function to redirect to the gallery 

        function goToGallery() { 

            window.location.href = 'gallery.html'; // Redirect to the gallery page 

        } 

    </script> 

</body> 

</html>
