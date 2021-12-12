# Welcome to Joseph Silva Jr.'s Pages

### Link Github Repository: 

https://github.com/MOJO1321/CS-499.git

# University

Southern New Hampshire University (SNHU)

# Class

Computer Science Capstone (CS 499)

# Video

Initial CS 499 Code Review -

Video to large to upload. Link for youtube is below:

[Link] https://youtu.be/1KiF2XPdkeg

# Polished Work

The raw data and code for these polished works along with the project can be found on this repository.

Link for Repository: https://github.com/MOJO1321/CS-499.git

### Software design/engineering

My project uses many files from libraries and files to be brought into the main.cpp file to create the design. For example, the use of shaderfiles were used to develop the 3D design of the objects in the 3D world and without these shaderfiles the program will not run due to an GL error. In order to not lose track of these shaderfiles, I placed a folder into the main project to retrieve these files whenever they are needed, and they can be used by anyone who has the project. Along with the shaderfile folder, I also placed an image folder with my jpg and png files to retrieve the images needed to wrap the texture around the 3D designs. 
One thing I changed from my original project; I added all my header files into the include directory of my project. Including these header files, allows the project to automatically retrieve the files without them being manually placed into the project within the sln for my project.


### Algorithms and data structures

I added new algorithms and data structures to my project to make the design better. With my design, I added new commands to the camera.h file to allow camera movement to up and down using the Q and E key on my keyboard by using the following commands with the GLFW library:

Main.cpp
![image](https://user-images.githubusercontent.com/76415618/145728786-ad5f088c-b7a6-4b48-ba59-aeb351d11769.png)

Camera.h
![image](https://user-images.githubusercontent.com/76415618/145728790-fd7ab1b9-8366-4038-9e8d-353b80d12cdd.png)


Also, I added data structures such as staticMesh3D.cpp and h files along with vertextBufferObject.cpp and h files to give images in my 3D design better graphics. The following is an example comparing a design from an earlier design of my project with my new one:

Older -
![image](https://user-images.githubusercontent.com/76415618/145728812-4821cd88-8d12-41b5-885f-06fbce9ba2b3.png)

Newer - 
![image](https://user-images.githubusercontent.com/76415618/145728817-a5a07032-f107-4392-ae6a-94a16fa26fb8.png)


Comparing the designs together, we can see the tile graphics are more realistic and more aligned in the newer version. We can also see the graphics on the duct tape and cellphone are a lot better as well when it comes to the shape and structure of it.

### Databases

![image](https://user-images.githubusercontent.com/76415618/145728665-d2881803-e304-42d4-91df-4d4d6d4e410e.png)

![image](https://user-images.githubusercontent.com/76415618/145728671-d8c45503-586d-4b99-9690-e5343f0826ac.png)

![image](https://user-images.githubusercontent.com/76415618/145728676-5816eb2c-c4c2-4ac3-b7a5-728438923065.png)

![image](https://user-images.githubusercontent.com/76415618/145728685-fdd37a41-7e68-4e73-9c1b-d6ae43d88c63.png)

![image](https://user-images.githubusercontent.com/76415618/145728690-e8b3b0a0-100a-4474-be72-237172940026.png)


These databases have set libraries which allow the use of many dynamic link libraries. These libraries contain many files such as hpp, h, c, and cpp files. These files are then allowed to be used with many programs when developing code. With the use of visual studios 2022 and cMaker, I was able to link these library folders and include folders into my project. In visual studios, these libraries are necessary to allow the creation of .exe programs, the development of a window, and math to create a 3D world. Throughout the first weeks of my capstone, my glew32.lib became corrupt and it was causing havoc to my project by creating errors and failures. Due to these libraries being open sources, I was able to get the newest version of my libraries and link the new libraries to my project. With these new libraries, I was able to add new algorithms and data structures to make my project even better by updating the project libraries to support x64 instead of x32. 

### Main Code (raw): 

Main.cpp Link: https://github.com/MOJO1321/CS-499/blob/59718d878e4e3a35c68d3ef0300f14667972f264/cpp%20files/Main.cpp

# Narrative

## Enhancement 1: Software Design/Engineering -

Raw data link: https://github.com/MOJO1321/CS-499/blob/efe87556631567bcaf13d5b5320f41dbb7da944a/Milestone2_Silva_Joseph.docx


### A. Briefly describe the artifact. What is it? When was it created? 

The artifacts are folders that were linked to the project through visual studios in order to have the project automatically retrieve these files during the operation. These files were header files, vs and fs files, jpg, and png files. The include folder I linked to the project contained many header files, which included mathematics from GLM, camera.h file, a 3D cylinder design file, etc. Along with the include folder, I also created an image folder, which contained the jpg and png files, and a shaderfile folder, which contained the vs and fs files. The two folders were placed in the main folder of the project and the files are automatically retrieved by the project instead of the project having to go through the computer to find these files. These folders were created at the beginning of this term in order for me to keep the entire project organized and to also have all the required files together with the project just in case it needed to be sent as a zip folder either by email or uploaded onto the internet.

Properties – VC++ Include – Include Directories – Library Include: ![image](https://user-images.githubusercontent.com/76415618/145728431-dc38ba87-780e-4910-b2b1-e83bd2c1bec4.png)

Include Folder: ![image](https://user-images.githubusercontent.com/76415618/145728449-5d0cfa4e-e34d-4ffa-a1b0-25bd6df72b69.png)

### B. Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved? 

I selected these items because these are the external files / folders that my project used in order to run properly. I had run into issues with having my files spread out on my computer when it came to running my program and also delivering my program to my professor. For example, if any of the files or folders were modified, the pathway to retrieve the data would malfunction and cause an error / failure in my project. Also, once I had sent the project over to my professor for a review, a lot of the files were missing, or the professor had to relink the pathways together in order for my project to work. 

These types of errors are not a large issue when it comes to working on a project by yourself, but when it comes to working with a team, these errors can cause a halt in production because the files are not attached with the main branch. I believe this showed my ability to be able to implement many different files whether created by myself, a team member, or an external party into my project very easily by just dropping the files into one directory instead of including multiple directories like we did in CS 330. Being able to make projects simple is a standard practice for new programmers and experienced ones. In the area below, I placed examples on how easy it was for my project to find certain files already included in the file by comparing a linker error. Please see arrows for the differences in photos.

Linker errors without proper pathway: (Shaderfiles example) - ![image](https://user-images.githubusercontent.com/76415618/145728467-0b70d7a9-dddc-4590-90d9-39231bf71d9b.png)

No errors with proper pathway: ![image](https://user-images.githubusercontent.com/76415618/145728474-0cf7870d-8a45-47ac-b4c1-7d84da2a6010.png)

### C. Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans? 

The enhancement did meet my plans for my enhancement because I can now easily implement many different files such as vertexbuffer and staticmesh3D header files into my project by just dropping it into the include folder without having to implement it into my project. For my updates, I have found the header files needed to add music to my project from irrklang. I was able to easily place the header files into the project. The header files for irrklang are not being implemented yet, but they are also not taking space in the header files area of visual studios in the project.

### D. Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?


When modifying my artifact, I learned it was a lot easier to implement new files into my project by adding the header files into the include folder because the include folder was already linked to my project. I did not have to add the header files into the actual project in visual studios because the project automatically retrieved the files since they were in the main project. One issue I had when I re-started my project was, I ran into libraries and files that were corrupted or malfunctioning since my original project used x32 and visual studios 2019 during my CS 330 class. For my CS 499, I had to use my own personal device instead of using Apporto virtual lab and I had to download visual studios 2022 with windows x64. This caused an issue with my linkers, directories, and libraries because I was using a different windows architecture than what was previously used. 

## Enhancement 2: Algorithms and Data Structure -

Raw data link: https://github.com/MOJO1321/CS-499/blob/8c4a501f11751f95b700312ed2afec99ce7511b9/Milestone3_Silva_Joseph.docx

### A. Briefly describe the artifact. What is it? When was it created? 

The artifacts that I added and modified to my project were header files and cpp files. The cpp and header files staticMesh3D and vertexBufferObject were implemented with the main.cpp and cylinder files in order to make the 3D designs inside my 3D world have better quality. These files were created approximately in 2014, but I found these files prior to my CS 499 class because I wanted to add to my project. The other file I modified was my main.cpp file and my camera.h file. The camera.h file was found on learnopengl site, during my CS 330 class. I modified these files in order to add new commands to my project. In my previous version of my project, the camera was only able to go left, right, forward, and backwards with the use of the keyboards and GLFW library. In the newer version, I added the camera to be able to move up and down as well.

### B. Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved? 


I selected these items because the 3D designs’ textures in the older version of my project were grainy, watery, and not correctly aligned. I was also having an issue with implementing images with higher pixels into my 3D designs and I had to go with lower quality imagery to complete the project. I also added new commands to the camera movement because I did not like how I had to use the scroll along with combining keyboard commands to make the camera view go up and down. These combinations of commands sometimes made my view of the 3D world at an unacceptable angle. The following are two photos comparing the 3D designs’ textures from the older and newer version of my project: 

Older Version - ![image](https://user-images.githubusercontent.com/76415618/145728486-34893569-79d2-4b8a-8b1c-140e5539a0e6.png)

Newer Version - ![image](https://user-images.githubusercontent.com/76415618/145728502-8b3c5f33-34c4-4efa-83ad-cd8ceccb7763.png)

The next is the code I implemented into my camera.h and main.cpp files in order to create the new commands. Please see arrows in photos for the modifications:

main.cpp - ![image](https://user-images.githubusercontent.com/76415618/145728517-5d886b30-40fc-4452-98eb-8428238e62b9.png)

camera.h - ![image](https://user-images.githubusercontent.com/76415618/145728526-59275fdf-92b5-4cd9-899c-858c49f39b07.png)

I believe these showed my abilities to locate open-source code and implementing the open-source code to my already created project by modifying it to fit with my original written code. The implemented code allowed me to update and upgrade my project to show and create better 3D design textures for any future project. The implementation of these additional codes and commands allows me or anyone using my open-source original code to have higher quality 3D texture designs with only making simple modifications within my original code to create a new 3D world by only having to worry about changing the vertices, indices, and image files. 

### C. Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans? 


The enhancement to my project by implementing additional header files and cpp files worked great. These files caused the 3D world and objects to looker higher in quality than my previous version of the project. I will be using header files from the learnopengl website 2D design to add sound affects and music to my 3D design to make my project seem more like a video game level than just an 3D art piece. The header files and cpp files have already been downloaded from irrklang opensource and I will be implementing them into my project.

### D. Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?


I learned I could enhance the design of my project by adding these open-source header files and cpp files. An issue I ran into when implementing these files were running into errors such as linker 2019 Microsoft errors. I placed the header files into the include folder and the cpp files into the main project, I also went into the header files and the cpp files to modify the codes on their pathway and their implementation into the main project. After modifying these areas, the project exe file worked like a charm.


## Enhancement 3: Databases -

### A. Briefly describe the artifact. What is it? When was it created? 


The artifacts that I re-modified to my project were the libraries for GLFW, GLM, GLEW, and GLAD. Earlier versions of these libraries were used in an earlier version of my OpenGL project, and I added the newer versions of these libraries during the start of CS 499.

### B. Justify the inclusion of the artifact in your ePortfolio. Why did you select this item? What specific components of the artifact showcase your skills and abilities in software development? How was the artifact improved? 


I added the newer versions of these libraries to my project for three major reasons. The first reason was because the older versions of these libraries were corrupted and prevented me from opening my project due to libraries such as opengl32.lib or glu32.lib. The second reason for updating the libraries was because I was able to add more features to my project such as GLAD allowing me to implement openGL version 4.5 instead of openGL 3.3 in my project, which allowed the project to have a better resolution. Also, the updated GLM library allowed an update on the mathematics being provided to the project. Lastly, the updated libraries for GLFW and GLEW allowed me to implement my project into visual studios 2022 instead of visual studios 2019, which allowed me to use a newer SDK version. I was also able to use the newer version of GLFW and GLEW to update my project from a x32 or 32-CPU system to a x64 or 64 CPU system, which allows my project to run faster and have better overall performance. The updates of these libraries allowed me to show my skills to use additional resources to find developed libraries to upgrade and update an already developed project to enhance it instead of starting over from scratch. I was also able to use other programs to help build the lib files such as using cMaker to develop the lib files for GLFW.

### C. Did you meet the course objectives you planned to meet with this enhancement in Module One? Do you have any updates to your outcome-coverage plans? 


The updating of the library files did meet my enhancement to change my project from a x32 bit to a x64 bit because it allowed my project to run faster by allocating more than 4GB of Ram while the project was running. Next, the updates allowed me to fix the corrupted lib files and they allowed my project to run with no errors.

### D. Reflect on the process of enhancing and/or modifying the artifact. What did you learn as you were creating it and improving it? What challenges did you face?


During this enhancement, I ran into a challenge with the GLFW library when using a x64 binary to create the lib files. In order to properly create these lib files, I used cMaker to develop a build for the GLFW library and linked the library to the 2022 visual studios. I learned my libraries had to be updated in my project because I was using a newer version of visual studios and without updating these libraries, my project ran into multiple errors and failures due to linker issues.

# Professional Self-Assessment

For my self-assessment, I started the computer science program at Southern New Hampshire University with little experience in computer science whether it was with hardware devices or software development. Throughout my journey at SNHU, I have learned many different computer languages such as C, C++, JAVA, JavaScript, Python, etc. and I have applied these languages to create programs in IDEs such as Eclipse, Visual Studio, JupyterNotebook, and PyCharm. These classes at SNHU helped me gain the knowledge in order to understand the skills required in a computer science career. I have also learned how to assemble and disassemble hardware devices when it comes to an IT career. When it comes to knowledge of programs and computer devices, I still have a lot to learn, but I am more diversed and educated then I was prior to starting this program.

In the area of experience, I am very new when it comes to having on-hands experience with computers and software development. Currently, I assist the State of California Computer Forensic Team in Law Enforcement where I have used programs and assembled/disassembled hardware devices in order to look for evidence for criminal activity. Prior, during, and after my journey at SNHU, I was a Law Enforcement officer (LEO) with the County of San Bernardino and then a Law Enforcement Officer with the State of California. During my time as a LEO, I investigated many computer crimes such as: embezzlement, theft, crimes against children, human trafficking, etc. and I have also testified in court for these cases to show how the evidence was collected from different areas such as: social media accounts, personal / business computers, smart phones, vehicles, etc. Besides investigations, I learned how to properly lead a team, conduct interviews, time management, and make quick desisions under stressful enviroments. When it comes to work experience, I do lack years of experience in computer science, but I have gained knowledge and experience from law enforcement where none to few canidates have compared to me.

For my future experience, I am hoping to continue to grow in my knowledge with computers by continuing my education with a Master's Degree in Cyber Security. I am also going to continue obtaining field-experience by applying as a full time investigator with the Computer Foresic Teams and this positions will allow me to attend more classes and seminars to gain additional education in the field of computers.

