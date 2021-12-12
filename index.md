# Welcome to Joseph Silva Jr.'s Pages


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

//libraries updated for CS 499 Milestone 4 by changing the libraries of GLFW, glad, Glew, and glm to x64 and the newest version. Please see project properties for the linker update.
// Please see pathway Project 3/libraries/lib & Project 3/libraries/include to find the libraries and include directories in the project for these reviews.

#include <glad/glad.h>
#include <GLFW/glfw3.h>
#define STB_IMAGE_IMPLEMENTATION
#include <stb_image.h>

#include <glm/glm.hpp>
#include <glm/gtc/matrix_transform.hpp>
#include <glm/gtc/type_ptr.hpp>

//Multiple header files placed in the included folder in main project - CS 499 Milestone 2
#include <shader.h>
#include <camera.h>

#include <iostream>

#include <cylinder.h>




void framebuffer_size_callback(GLFWwindow* window, int width, int height);
void mouse_callback(GLFWwindow* window, double xpos, double ypos);
void scroll_callback(GLFWwindow* window, double xoffset, double yoffset);
void processInput(GLFWwindow* window);
unsigned int loadTexture(const char* path);


// settings
const unsigned int SCR_WIDTH = 800;
const unsigned int SCR_HEIGHT = 600;


// camera
glm::vec3 cameraPos = glm::vec3(0.0f, 0.0f, 3.0f);
glm::vec3 cameraFront = glm::vec3(0.0f, 0.0f, -1.0f);
glm::vec3 cameraUp = glm::vec3(0.0f, 1.0f, 0.0f);

bool firstMouse = true;
float yaw = -90.0f;	// yaw is initialized to -90.0 degrees since a yaw of 0.0 results in a direction vector pointing to the right so we initially rotate a bit to the left.
float pitch = 0.0f;
float lastX = 800.0f / 2.0;
float lastY = 600.0 / 2.0;
float fov = 45.0f;

// timing
float deltaTime = 0.0f;	// time between current frame and last frame
float lastFrame = 0.0f;

// lighting
glm::vec3 lightPos(-3.5f, 0.0f, -3.7f);

int main()
{
    // glfw: initialize and configure
    // ------------------------------
    glfwInit();
    glfwWindowHint(GLFW_CONTEXT_VERSION_MAJOR, 3);
    glfwWindowHint(GLFW_CONTEXT_VERSION_MINOR, 3);
    glfwWindowHint(GLFW_OPENGL_PROFILE, GLFW_OPENGL_CORE_PROFILE);

#ifdef __APPLE__
    glfwWindowHint(GLFW_OPENGL_FORWARD_COMPAT, GL_TRUE);
#endif

    // glfw window creation
    // --------------------
    GLFWwindow* window = glfwCreateWindow(SCR_WIDTH, SCR_HEIGHT, "Project", NULL, NULL);
    if (window == NULL)
    {
        std::cout << "Failed to create GLFW window" << std::endl;
        glfwTerminate();
        return -1;
    }

    glfwMakeContextCurrent(window);
    glfwSetFramebufferSizeCallback(window, framebuffer_size_callback);
    glfwSetCursorPosCallback(window, mouse_callback);
    glfwSetScrollCallback(window, scroll_callback);

    // tell GLFW to capture our mouse
    glfwSetInputMode(window, GLFW_CURSOR, GLFW_CURSOR_DISABLED);

    // glad: load all OpenGL function pointers
    // ---------------------------------------
    if (!gladLoadGLLoader((GLADloadproc)glfwGetProcAddress))
    {
        std::cout << "Failed to initialize GLAD" << std::endl;
        return -1;
    }

    // configure global opengl state
    // -----------------------------
    glEnable(GL_DEPTH_TEST);

    // build and compile our shader zprogram
    // ------------------------------------
    //shader files placed in the shaderfile folder in main project - CS 499 Milestone 2
    Shader lightingShader("shaderfiles/6.multiple_lights.vs", "shaderfiles/6.multiple_lights.fs");
    Shader lightCubeShader("shaderfiles/6.light_cube.vs", "shaderfiles/6.light_cube.fs");


    float vertices[] = {
        // positions          //normal       // texture coords
        // plane counter top
        -5.0f, -5.0f, -5.0f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
        -5.0f, -5.0f,  5.0f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         5.0f, -5.0f,  5.0f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
         5.0f, -5.0f, -5.0f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

         //Cell Phone Body

         2.2f, -4.99f,  0.5f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
         1.8f, -4.99f,  3.5f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         2.8f, -4.99f,  3.5f, 0.0f,  0.0f, -1.0f,      1.0f, 0.0f, // bottom right
         3.2f, -4.99f,  0.5f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

         2.2f, -4.7f,  0.5f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
         1.8f, -4.7f,  3.5f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         2.8f, -4.7f,  3.5f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
         3.2f, -4.7f,  0.5f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

         //Cell Phone Screen

         2.25f, -4.7f,  0.55f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
         1.85f, -4.7f,  3.45f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         2.75f, -4.7f,  3.45f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
         3.15f, -4.7f,  0.55f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

         //tissue box

        -4.0f, -4.99f, -3.0f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
        -3.0f, -4.99f,  0.0f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         1.0f, -4.99f, -1.0f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
         0.0f, -4.99f, -4.0f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

        -4.0f, -4.0f, -3.0f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
        -3.0f, -4.0f,  0.0f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // bottom left
         1.0f, -4.0f, -1.0f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
         0.0f, -4.0f, -4.0f, 0.0f,  0.0f, -1.0f,       1.0f, 1.0f, // top right

         //tissue box hole

        -2.5f, -3.9f,  -2.05f, 0.0f,  0.0f, -1.0f,     0.0f, 1.0f, // top left
        -2.25f, -3.9f, -1.30f, 0.0f,  0.0f, -1.0f,     0.0f, 0.0f, // bottom left
        -0.65f, -3.9f, -1.75f, 0.0f,  0.0f, -1.0f,     1.0f, 0.0f, // bottom right
        -0.90f, -3.9f, -2.50f, 0.0f,  0.0f, -1.0f,     1.0f, 1.0f, // top right

        //foam brush head #1

        -1.5f, -4.99f,  1.5f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
        -1.0f, -4.99f,  1.95f, 0.0f,  0.0f, -1.0f,      0.0f, 0.0f, // bottom left
        -0.5f, -4.99f,  1.1f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
        -0.95f, -4.99f, 0.55f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // top right

        -1.5f, -4.65f,  1.5f, 0.0f,  0.0f, -1.0f,      0.0f, 1.0f, // top left
        -1.0f,  -4.65f,  1.95f, 0.0f,  0.0f, -1.0f,     0.0f, 0.0f, // bottom left
        -0.64f,  -4.65f, 1.31f, 0.0f,  0.0f, -1.0f,      1.0f, 0.0f, // bottom right
        -1.05f, -4.65f,  0.85f, 0.0f,  0.0f, -1.0f,     1.0f, 1.0f, // top right

        -1.0f, -4.99f,  1.95f, 0.0f,  0.0f, -1.0f,      0.0f, 0.0f, // bottom left
        -0.5f, -4.99f,  1.1f,  0.0f,  0.0f, -1.0f,      1.0f, 0.0f, // bottom right
        -1.0f,  -4.65f,  1.95f, 0.0f,  0.0f, -1.0f,     0.0f, 1.0f, // bottom left
        -0.64f,  -4.65f, 1.31f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // bottom right

        -0.5f, -4.99f,  1.1f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
        -0.95f, -4.99f, 0.55f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // top right
        -0.64f,  -4.65f, 1.31f, 0.0f,  0.0f, -1.0f,    0.0f, 0.0f, // bottom right
        -1.05f, -4.65f,  0.85f, 0.0f,  0.0f, -1.0f,    0.0f, 1.0f, // top right

        -1.5f, -4.99f,  1.5f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // top left
        -1.0f, -4.99f,  1.95f, 0.0f,  0.0f, -1.0f,      1.0f, 0.0f, // bottom left
        -1.5f, -4.65f,  1.5f, 0.0f,  0.0f, -1.0f,      0.0f, 1.0f, // top left
        -1.0f,  -4.65f,  1.95f, 0.0f,  0.0f, -1.0f,    1.0f, 1.0f, // bottom left

        -1.5f, -4.99f,  1.5f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // top left
        -1.5f, -4.65f,  1.5f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // top left
        -0.95f, -4.99f, 0.55f, 0.0f,  0.0f, -1.0f,      0.0f, 0.0f, // top right
        -1.05f, -4.65f,  0.85f, 0.0f,  0.0f, -1.0f,    0.0f, 1.0f, // top right

        //foam brush head #2

        -2.0f, -4.99f,  1.0f, 0.0f,  0.0f, -1.0f,       0.0f, 1.0f, // top left
        -1.5f, -4.99f,  1.45f, 0.0f,  0.0f, -1.0f,      0.0f, 0.0f, // bottom left
        -1.0f, -4.99f,  0.6f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
        -1.45f, -4.99f, 0.05f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // top right

        -2.0f, -4.65f,   1.0f, 0.0f,  0.0f, -1.0f,      0.0f, 1.0f, // top left
        -1.5f,  -4.65f,  1.45f, 0.0f,  0.0f, -1.0f,     0.0f, 0.0f, // bottom left
        -1.14f,  -4.65f, 0.81f, 0.0f,  0.0f, -1.0f,     1.0f, 0.0f, // bottom right
        -1.55f, -4.65f,  0.35f, 0.0f,  0.0f, -1.0f,     1.0f, 1.0f, // top right

        -1.5f, -4.99f,  1.45f, 0.0f,  0.0f, -1.0f,      0.0f, 0.0f, // bottom left
        -1.0f, -4.99f,  0.6f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
        -1.5f,  -4.65f,  1.45f, 0.0f,  0.0f, -1.0f,     0.0f, 1.0f, // bottom left
        -1.14f,  -4.65f, 0.81f, 0.0f,  0.0f, -1.0f,     1.0f, 1.0f, // bottom right

        -1.0f, -4.99f,  0.6f, 0.0f,  0.0f, -1.0f,       1.0f, 0.0f, // bottom right
        -1.45f, -4.99f, 0.05f, 0.0f,  0.0f, -1.0f,      1.0f, 1.0f, // top right
        -1.14f,  -4.65f, 0.81f, 0.0f,  0.0f, -1.0f,     0.0f, 0.0f, // bottom right
        -1.55f, -4.65f,  0.35f, 0.0f,  0.0f, -1.0f,     0.0f, 1.0f, // top right

        -2.0f, -4.99f,  1.0f, 0.0f,  0.0f, -1.0f,       0.0f, 0.0f, // top left
        -1.5f, -4.99f,  1.45f, 0.0f, 0.0f, -1.0f, 1.0f, 0.0f, // bottom left
        -2.0f, -4.65f,   1.0f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f, // top left
        -1.5f,  -4.65f,  1.45f, 0.0f, 0.0f, -1.0f, 1.0f, 1.0f, // bottom left

        -2.0f, -4.99f,  1.0f, 0.0f, 0.0f, -1.0f, 1.0f, 0.0f, // top left
        -2.0f, -4.65f,   1.0f, 0.0f, 0.0f, -1.0f, 1.0f, 1.0f, // top left
        -1.45f, -4.99f, 0.05f, 0.0f, 0.0f, -1.0f, 0.0f, 0.0f, // top right
        -1.55f, -4.65f,  0.35f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f, // top right

        //Pen Tip

       -0.92f, -4.95f,  2.22f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,
       -0.82f, -4.998f,   2.27f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,
       -0.87f, -4.998f,  2.34f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,

       -0.92f, -4.95f, 2.22f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,
       -0.82f,  -4.92f, 2.27f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,
       -0.87f,  -4.92f, 2.34f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,

       //Duct tape

       2.1f, -4.48f, -2.2f, 0.0f, 0.0f, -1.0f, 0.0f, 1.0f,
       3.5f, -4.48f, -0.8f, 0.0f, 0.0f, -1.0f, 1.0f, 0.0f,
       3.5f, -4.48f, -2.2f, 0.0f, 0.0f, -1.0f, 1.0f, 1.0f,
       2.1f, -4.48f, -0.8f, 0.0f, 0.0f, -1.0f, 0.0f, 0.0f,

       //light cube

       -0.5f, -3.5f, -0.5f,  0.0f,  0.0f, -1.0f,  0.0f,  0.0f,
        0.5f, -3.5f, -0.5f,  0.0f,  0.0f, -1.0f,  1.0f,  0.0f,
        0.5f, -2.5f, -0.5f,  0.0f,  0.0f, -1.0f,  1.0f,  1.0f,
        0.5f, -2.5f, -0.5f,  0.0f,  0.0f, -1.0f,  1.0f,  1.0f,
       -0.5f, -2.5f, -0.5f,  0.0f,  0.0f, -1.0f,  0.0f,  1.0f,
       -0.5f, -3.5f, -0.5f,  0.0f,  0.0f, -1.0f,  0.0f,  0.0f,

       -0.5f, -3.5f,  0.5f,  0.0f,  0.0f,  1.0f,  0.0f,  0.0f,
        0.5f, -3.5f,  0.5f,  0.0f,  0.0f,  1.0f,  1.0f,  0.0f,
        0.5f, -2.5f,  0.5f,  0.0f,  0.0f,  1.0f,  1.0f,  1.0f,
        0.5f, -2.5f,  0.5f,  0.0f,  0.0f,  1.0f,  1.0f,  1.0f,
       -0.5f, -2.5f,  0.5f,  0.0f,  0.0f,  1.0f,  0.0f,  1.0f,
       -0.5f, -3.5f,  0.5f,  0.0f,  0.0f,  1.0f,  0.0f,  0.0f,

       -0.5f, -2.5f,  0.5f, -1.0f,  0.0f,  0.0f,  1.0f,  0.0f,
       -0.5f, -2.5f, -0.5f, -1.0f,  0.0f,  0.0f,  1.0f,  1.0f,
       -0.5f, -3.5f, -0.5f, -1.0f,  0.0f,  0.0f,  0.0f,  1.0f,
       -0.5f, -3.5f, -0.5f, -1.0f,  0.0f,  0.0f,  0.0f,  1.0f,
       -0.5f, -3.5f,  0.5f, -1.0f,  0.0f,  0.0f,  0.0f,  0.0f,
       -0.5f, -2.5f,  0.5f, -1.0f,  0.0f,  0.0f,  1.0f,  0.0f,

        0.5f, -2.5f,  0.5f,  1.0f,  0.0f,  0.0f,  1.0f,  0.0f,
        0.5f, -2.5f, -0.5f,  1.0f,  0.0f,  0.0f,  1.0f,  1.0f,
        0.5f, -3.5f, -0.5f,  1.0f,  0.0f,  0.0f,  0.0f,  1.0f,
        0.5f, -3.5f, -0.5f,  1.0f,  0.0f,  0.0f,  0.0f,  1.0f,
        0.5f, -3.5f,  0.5f,  1.0f,  0.0f,  0.0f,  0.0f,  0.0f,
        0.5f, -2.5f,  0.5f,  1.0f,  0.0f,  0.0f,  1.0f,  0.0f,

       -0.5f, -3.5f, -0.5f,  0.0f, -1.0f,  0.0f,  0.0f,  1.0f,
        0.5f, -3.5f, -0.5f,  0.0f, -1.0f,  0.0f,  1.0f,  1.0f,
        0.5f, -3.5f,  0.5f,  0.0f, -1.0f,  0.0f,  1.0f,  0.0f,
        0.5f, -3.5f,  0.5f,  0.0f, -1.0f,  0.0f,  1.0f,  0.0f,
       -0.5f, -3.5f,  0.5f,  0.0f, -1.0f,  0.0f,  0.0f,  0.0f,
       -0.5f, -3.5f, -0.5f,  0.0f, -1.0f,  0.0f,  0.0f,  1.0f,

       -0.5f, -2.5f, -0.5f,  0.0f,  1.0f,  0.0f,  0.0f,  1.0f,
        0.5f, -2.5f, -0.5f,  0.0f,  1.0f,  0.0f,  1.0f,  1.0f,
        0.5f, -2.5f,  0.5f,  0.0f,  1.0f,  0.0f,  1.0f,  0.0f,
        0.5f, -2.5f,  0.5f,  0.0f,  1.0f,  0.0f,  1.0f,  0.0f,
       -0.5f, -2.5f,  0.5f,  0.0f,  1.0f,  0.0f,  0.0f,  0.0f,
       -0.5f, -2.5f, -0.5f,  0.0f,  1.0f,  0.0f,  0.0f,  1.0f

    };

    unsigned int indices[] = {

        //counter top
        0,1,2,
        0,2,3,

        //cell phone body
        4,5,6,
        4,6,7,
        4,8,9,
        4,5,9,
        4,7,8,
        7,8,11,
        5,6,9,
        6,9,10,
        6,7,11,
        6,10,11,

        //cell phone screen
        12,13,14,
        12,14,15,

        //tissue box
        16,17,18,
        16,18,19,
        20,21,22,
        20,22,23,
        16,19,20,
        19,20,23,
        16,17,20,
        17,20,21,
        17,18,21,
        18,21,22,
        18,19,22,
        19,22,23,

        //tissue box hole
        24,25,26,
        24,26,27,

        //foam brush head #1
        28,29,30,
        28,30,31,
        32,33,34,
        32,34,35,
        36,37,38,
        37,38,39,
        40,41,42,
        41,42,43,
        44,45,46,
        45,46,47,
        48,49,50,
        49,50,51,

        //foam brush head #2
        52,53,54,
        52,54,55,
        56,57,58,
        56,58,59,
        60,61,62,
        61,62,63,
        64,65,66,
        65,66,67,
        68,69,70,
        69,70,71,
        72,73,74,
        73,74,75,

        //pen tip
        76,77,78,
        79,80,81,
        76,78,81,
        79,77,80,

        //duct tape
        82,83,85,
        82,83,84,

    };

    // positions of the point lights
    glm::vec3 pointLightPositions[] = {
        glm::vec3(4.0f,  -4.0f,  -4.0f),
        glm::vec3(-4.0f, -4.0f,  4.0f),
        glm::vec3(4.0f,  -4.0f, 4.0f),
        glm::vec3(-4.0f,  -4.0f, -4.0f)
    };

    unsigned int VBO, VAO, EBO;
    unsigned int VBO2, VAO2;
    unsigned int VBO3, VAO3;


    glGenVertexArrays(1, &VAO);
    glGenBuffers(1, &VBO);
    glGenBuffers(1, &EBO);
    glBindVertexArray(VAO);
    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    glBufferData(GL_ARRAY_BUFFER, sizeof(vertices), vertices, GL_STATIC_DRAW);
    glBindBuffer(GL_ELEMENT_ARRAY_BUFFER, EBO);
    glBufferData(GL_ELEMENT_ARRAY_BUFFER, sizeof(indices), indices, GL_STATIC_DRAW);


    // position attribute
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);
    // position attribute
    glVertexAttribPointer(1, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(3 * sizeof(float)));
    glEnableVertexAttribArray(1);
    // texture coord attribute
    glVertexAttribPointer(2, 2, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)(6 * sizeof(float)));
    glEnableVertexAttribArray(2);

    glGenVertexArrays(1, &VAO2);
    glGenBuffers(1, &VBO2);
    glBindVertexArray(VAO2);
    glBindBuffer(GL_ARRAY_BUFFER, VBO2);


    unsigned int lightCubeVAO;
    glGenVertexArrays(1, &lightCubeVAO);
    glBindVertexArray(lightCubeVAO);

    glBindBuffer(GL_ARRAY_BUFFER, VBO);
    // note that we update the lamp's position attribute's stride to reflect the updated buffer data
    glVertexAttribPointer(0, 3, GL_FLOAT, GL_FALSE, 8 * sizeof(float), (void*)0);
    glEnableVertexAttribArray(0);

    // load textures (we now use a utility function to keep the code more organized)
    // -----------------------------------------------------------------------------
    unsigned int diffuseMap = loadTexture("images/tile.jpg");
    unsigned int specularMap = loadTexture("images/tile.jpg");

    // shader configuration
    // --------------------
    lightingShader.use();
    lightingShader.setInt("material.diffuse", 0);
    lightingShader.setInt("material.specular", 1);

    // load and create a texture 
       // -------------------------
    //image files placed in the image folder in main project - CS 499 Milestone 2
    unsigned int texture1, texture2, texture3, texture4, texture5, texture6, texture7, texture8, texture9;

    // texture 1
    // ---------
    glGenTextures(1, &texture1);
    glBindTexture(GL_TEXTURE_2D, texture1);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    int width, height, nrChannels;
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    unsigned char* data = stbi_load("images/GIC1.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 2
// ---------
    glGenTextures(1, &texture2);
    glBindTexture(GL_TEXTURE_2D, texture2);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/IS.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 3
// ---------
    glGenTextures(1, &texture3);
    glBindTexture(GL_TEXTURE_2D, texture3);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/pb1.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 4
// ---------
    glGenTextures(1, &texture4);
    glBindTexture(GL_TEXTURE_2D, texture4);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/foam.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 5
// ---------
    glGenTextures(1, &texture5);
    glBindTexture(GL_TEXTURE_2D, texture5);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/silver1.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 6
// ---------
    glGenTextures(1, &texture6);
    glBindTexture(GL_TEXTURE_2D, texture6);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/black.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 7
// ---------
    glGenTextures(1, &texture7);
    glBindTexture(GL_TEXTURE_2D, texture7);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/white.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 8
// ---------
    glGenTextures(1, &texture8);
    glBindTexture(GL_TEXTURE_2D, texture8);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/wood.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);

    // texture 8
// ---------
    glGenTextures(1, &texture9);
    glBindTexture(GL_TEXTURE_2D, texture9);
    // set the texture wrapping parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
    // set texture filtering parameters
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR);
    glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);
    // load image, create texture and generate mipmaps
    stbi_set_flip_vertically_on_load(true); // tell stb_image.h to flip loaded texture's on the y-axis.
    data = stbi_load("images/ducttape.png", &width, &height, &nrChannels, 0);
    if (data)
    {
        glTexImage2D(GL_TEXTURE_2D, 0, GL_RGBA, width, height, 0, GL_RGBA, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);
    }
    else
    {
        std::cout << "Failed to load texture" << std::endl;
    }
    stbi_image_free(data);



    // tell opengl for each sampler to which texture unit it belongs to (only has to be done once)
    // -------------------------------------------------------------------------------------------
    lightingShader.use();
    lightingShader.setInt("material.diffuse", 0);
    lightingShader.setInt("material.specular", 1);
    lightingShader.setInt("texture1", 2);
    lightingShader.setInt("texture2", 3);
    lightingShader.setInt("texture3", 4);
    lightingShader.setInt("texture4", 5);
    lightingShader.setInt("texture5", 6);
    lightingShader.setInt("texture6", 7);
    lightingShader.setInt("texture7", 8);
    lightingShader.setInt("texture8", 9);
    lightingShader.setInt("texture9", 10);


    glm::mat4 model;
    float angle;

    //

    // render loop
    // -----------
    while (!glfwWindowShouldClose(window))
    {
        // per-frame time logic
        // --------------------
        float currentFrame = glfwGetTime();
        deltaTime = currentFrame - lastFrame;
        lastFrame = currentFrame;

        // input
        // -----
        processInput(window);

        glClearColor(0.0f, 0.0f, 0.0f, 1.0f);
        glClear(GL_COLOR_BUFFER_BIT | GL_DEPTH_BUFFER_BIT);

        // light on the plane for the tile

        // activate shader
        lightingShader.use();
        lightingShader.setVec3("viewPos", cameraPos);
        lightingShader.setFloat("material.shininess", 32.0f);

        lightingShader.setVec3("dirLight.direction", 0.0f, -5.0f, 0.0f);
        lightingShader.setVec3("dirLight.ambient", 0.1f, 0.1f, 0.1f);
        lightingShader.setVec3("dirLight.diffuse", 0.4f, 0.4f, 0.4f);
        lightingShader.setVec3("dirLight.specular", 0.8f, 0.8f, 0.8f);
        // point light 1
        lightingShader.setVec3("pointLights[0].position", pointLightPositions[0]);
        lightingShader.setVec3("pointLights[0].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[0].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[0].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[0].constant", 1.0f);
        lightingShader.setFloat("pointLights[0].linear", 0.09);
        lightingShader.setFloat("pointLights[0].quadratic", 0.032);
        // point light 2
        lightingShader.setVec3("pointLights[1].position", pointLightPositions[1]);
        lightingShader.setVec3("pointLights[1].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[1].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[1].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[1].constant", 1.0f);
        lightingShader.setFloat("pointLights[1].linear", 0.09);
        lightingShader.setFloat("pointLights[1].quadratic", 0.032);
        // point light 3
        lightingShader.setVec3("pointLights[2].position", pointLightPositions[2]);
        lightingShader.setVec3("pointLights[2].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[2].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[2].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[2].constant", 1.0f);
        lightingShader.setFloat("pointLights[2].linear", 0.09);
        lightingShader.setFloat("pointLights[2].quadratic", 0.032);
        // point light 4
        lightingShader.setVec3("pointLights[3].position", pointLightPositions[3]);
        lightingShader.setVec3("pointLights[3].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[3].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[3].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[3].constant", 1.0f);
        lightingShader.setFloat("pointLights[3].linear", 0.09);
        lightingShader.setFloat("pointLights[3].quadratic", 0.032);
        // spotLight
        lightingShader.setVec3("spotLight.position", cameraPos);
        lightingShader.setVec3("spotLight.direction", cameraFront);
        lightingShader.setVec3("spotLight.ambient", 0.0f, 0.0f, 0.0f);
        lightingShader.setVec3("spotLight.diffuse", 1.0f, 1.0f, 1.0f);
        lightingShader.setVec3("spotLight.specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("spotLight.constant", 1.0f);
        lightingShader.setFloat("spotLight.linear", 0.09);
        lightingShader.setFloat("spotLight.quadratic", 0.032);
        lightingShader.setFloat("spotLight.cutOff", glm::cos(glm::radians(12.5f)));
        lightingShader.setFloat("spotLight.outerCutOff", glm::cos(glm::radians(15.0f)));        // activate shader
        lightingShader.use();
        lightingShader.setVec3("viewPos", cameraPos);
        lightingShader.setFloat("material.shininess", 32.0f);

        lightingShader.setVec3("dirLight.direction", 0.0f, -5.0f, 0.0f);
        lightingShader.setVec3("dirLight.ambient", 0.1f, 0.1f, 0.1f);
        lightingShader.setVec3("dirLight.diffuse", 0.4f, 0.4f, 0.4f);
        lightingShader.setVec3("dirLight.specular", 0.8f, 0.8f, 0.8f);
        // point light 1
        lightingShader.setVec3("pointLights[0].position", pointLightPositions[0]);
        lightingShader.setVec3("pointLights[0].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[0].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[0].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[0].constant", 1.0f);
        lightingShader.setFloat("pointLights[0].linear", 0.09);
        lightingShader.setFloat("pointLights[0].quadratic", 0.032);
        // point light 2
        lightingShader.setVec3("pointLights[1].position", pointLightPositions[1]);
        lightingShader.setVec3("pointLights[1].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[1].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[1].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[1].constant", 1.0f);
        lightingShader.setFloat("pointLights[1].linear", 0.09);
        lightingShader.setFloat("pointLights[1].quadratic", 0.032);
        // point light 3
        lightingShader.setVec3("pointLights[2].position", pointLightPositions[2]);
        lightingShader.setVec3("pointLights[2].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[2].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[2].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[2].constant", 1.0f);
        lightingShader.setFloat("pointLights[2].linear", 0.09);
        lightingShader.setFloat("pointLights[2].quadratic", 0.032);
        // point light 4
        lightingShader.setVec3("pointLights[3].position", pointLightPositions[3]);
        lightingShader.setVec3("pointLights[3].ambient", 0.3f, 0.3f, 0.3f);
        lightingShader.setVec3("pointLights[3].diffuse", 0.8f, 0.8f, 0.8f);
        lightingShader.setVec3("pointLights[3].specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("pointLights[3].constant", 1.0f);
        lightingShader.setFloat("pointLights[3].linear", 0.09);
        lightingShader.setFloat("pointLights[3].quadratic", 0.032);
        // spotLight
        lightingShader.setVec3("spotLight.position", cameraPos);
        lightingShader.setVec3("spotLight.direction", cameraFront);
        lightingShader.setVec3("spotLight.ambient", 0.0f, 0.0f, 0.0f);
        lightingShader.setVec3("spotLight.diffuse", 1.0f, 1.0f, 1.0f);
        lightingShader.setVec3("spotLight.specular", 1.0f, 1.0f, 1.0f);
        lightingShader.setFloat("spotLight.constant", 1.0f);
        lightingShader.setFloat("spotLight.linear", 0.09);
        lightingShader.setFloat("spotLight.quadratic", 0.032);
        lightingShader.setFloat("spotLight.cutOff", glm::cos(glm::radians(12.5f)));
        lightingShader.setFloat("spotLight.outerCutOff", glm::cos(glm::radians(15.0f)));


        // pass projection matrix to shader (note that in this case it could change every frame)
        glm::mat4 projection = glm::perspective(glm::radians(fov), (float)SCR_WIDTH / (float)SCR_HEIGHT, 0.1f, 100.0f);
        lightingShader.setMat4("projection", projection);

        // camera/view transformation
        glm::mat4 view = glm::lookAt(cameraPos, cameraPos + cameraFront, cameraUp);
        lightingShader.setMat4("view", view);


        glBindVertexArray(VAO);
        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        // bind diffuse map
        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, diffuseMap);
        // bind specular map
        glActiveTexture(GL_TEXTURE1);
        glBindTexture(GL_TEXTURE_2D, specularMap);

        glDrawElements(GL_TRIANGLES, 6, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);


        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture1);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 38, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture2);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 42, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture3);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 80, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture6);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 84, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture4);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 158, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture5);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 170, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture9);
        glBindVertexArray(VAO);

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        angle = 0.0f;
        model = glm::rotate(model, glm::radians(angle), glm::vec3(1.0f, 0.3f, 0.5f));
        lightingShader.setMat4("model", model);

        glDrawElements(GL_TRIANGLES, 200, GL_UNSIGNED_INT, 0);
        glBindVertexArray(0);

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture6);
        glBindVertexArray(VAO2);
        model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(0.0f, -1.74f, 0.0f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C(0.1, 100, 0.5, true, true, true);
        C.render();

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture7);
        glBindVertexArray(VAO2);
        model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(0.0f, -1.39f, 0.0f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C2(0.1, 100, 0.2, true, true, true);
        C2.render();

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture8);
        glBindVertexArray(VAO2);
        glm::mat4 model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(-2.0f, -1.8f, 1.63f));
        model = glm::rotate(model, glm::radians(90.0f), glm::vec3(1.2f, 0.0f, 0.8f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C3(0.07, 100, 1.0, true, true, true);
        C3.render();

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture8);
        glBindVertexArray(VAO2);
        model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(-1.48f, -1.8f, 2.11f));
        model = glm::rotate(model, glm::radians(90.0f), glm::vec3(1.2f, 0.0f, 0.8f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C4(0.07, 100, 1.0, true, true, true);
        C4.render();

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture6);
        glBindVertexArray(VAO2);
        model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(-0.5f, -1.96f, 2.65f));
        model = glm::rotate(model, glm::radians(90.0f), glm::vec3(-0.2f, 0.0f, 0.2f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C5(0.04, 100, 1.0, true, true, true);
        C5.render();

        glActiveTexture(GL_TEXTURE0);
        glBindTexture(GL_TEXTURE_2D, texture6);
        glBindVertexArray(VAO2);
        model = glm::mat4(1.0f);
        model = glm::translate(model, glm::vec3(2.8f, -1.74f, -1.5f));
        lightingShader.setMat4("model", model);

        static_meshes_3D::Cylinder C6(1, 100, 0.5, true, true, true);
        C6.render();

        // create transformations
        model = glm::mat4(1.0f); // make sure to initialize matrix to identity matrix first
        model = glm::translate(model, glm::vec3(0.0f, 3.0f, 0.0f));
        lightingShader.setMat4("model", model);

        // also draw the lamp object
        lightCubeShader.use();
        lightCubeShader.setMat4("projection", projection);
        lightCubeShader.setMat4("view", view);
        model = glm::mat4(1.0f);
        model = glm::translate(model, lightPos);
        model = glm::scale(model, glm::vec3(0.2f)); // a smaller cube
        lightCubeShader.setMat4("model", model);

        glBindVertexArray(lightCubeVAO);
        glDrawArrays(GL_TRIANGLES, 86, 36);


        // glfw: swap buffers and poll IO events (keys pressed/released, mouse moved etc.)
        // -------------------------------------------------------------------------------
        glfwSwapBuffers(window);
        glfwPollEvents();
    }

    // optional: de-allocate all resources once they've outlived their purpose:
    // ------------------------------------------------------------------------
    glDeleteVertexArrays(1, &VAO);
    glDeleteVertexArrays(1, &VAO2);
    glDeleteVertexArrays(1, &lightCubeVAO);
    glDeleteBuffers(1, &VBO);
    glDeleteBuffers(1, &VBO2);
    glDeleteBuffers(1, &EBO);



    // glfw: terminate, clearing all previously allocated GLFW resources.
    // ------------------------------------------------------------------
    glfwTerminate();
    return 0;

}

// process all input: query GLFW whether relevant keys are pressed/released this frame and react accordingly
// ---------------------------------------------------------------------------------------------------------
void processInput(GLFWwindow* window)
{
    if (glfwGetKey(window, GLFW_KEY_ESCAPE) == GLFW_PRESS)
        glfwSetWindowShouldClose(window, true);

    float cameraSpeed = 2.5 * deltaTime;
    if (glfwGetKey(window, GLFW_KEY_W) == GLFW_PRESS)
        cameraPos += cameraSpeed * cameraFront;
    if (glfwGetKey(window, GLFW_KEY_S) == GLFW_PRESS)
        cameraPos -= cameraSpeed * cameraFront;
    if (glfwGetKey(window, GLFW_KEY_A) == GLFW_PRESS)
        cameraPos -= glm::normalize(glm::cross(cameraFront, cameraUp)) * cameraSpeed;
    if (glfwGetKey(window, GLFW_KEY_D) == GLFW_PRESS)
        cameraPos += glm::normalize(glm::cross(cameraFront, cameraUp)) * cameraSpeed;
    // CS 499 Milestone 3 commands added 
    if (glfwGetKey(window, GLFW_KEY_Q) == GLFW_PRESS)
        cameraPos += cameraSpeed * cameraUp;
    if (glfwGetKey(window, GLFW_KEY_E) == GLFW_PRESS)
        cameraPos -= cameraSpeed * cameraUp;

}

// glfw: whenever the window size changed (by OS or user resize) this callback function executes
// ---------------------------------------------------------------------------------------------
void framebuffer_size_callback(GLFWwindow* window, int width, int height)
{
    // make sure the viewport matches the new window dimensions; note that width and 
    // height will be significantly larger than specified on retina displays.
    glViewport(0, 0, width, height);

}

// glfw: whenever the mouse moves, this callback is called
// -------------------------------------------------------
void mouse_callback(GLFWwindow* window, double xpos, double ypos)
{
    if (firstMouse)
    {
        lastX = xpos;
        lastY = ypos;
        firstMouse = false;
    }

    float xoffset = xpos - lastX;
    float yoffset = lastY - ypos; // reversed since y-coordinates go from bottom to top
    lastX = xpos;
    lastY = ypos;

    float sensitivity = 0.1f; // change this value to your liking
    xoffset *= sensitivity;
    yoffset *= sensitivity;

    yaw += xoffset;
    pitch += yoffset;

    // make sure that when pitch is out of bounds, screen doesn't get flipped
    if (pitch > 89.0f)
        pitch = 89.0f;
    if (pitch < -89.0f)
        pitch = -89.0f;

    glm::vec3 front;
    front.x = cos(glm::radians(yaw)) * cos(glm::radians(pitch));
    front.y = sin(glm::radians(pitch));
    front.z = sin(glm::radians(yaw)) * cos(glm::radians(pitch));
    cameraFront = glm::normalize(front);
}

// glfw: whenever the mouse scroll wheel scrolls, this callback is called
// ----------------------------------------------------------------------
void scroll_callback(GLFWwindow* window, double xoffset, double yoffset)
{
    fov -= (float)yoffset;
    if (fov < 1.0f)
        fov = 1.0f;
    if (fov > 45.0f)
        fov = 45.0f;
}

unsigned int loadTexture(char const* path)
{
    unsigned int textureID;
    glGenTextures(1, &textureID);

    int width, height, nrComponents;
    unsigned char* data = stbi_load(path, &width, &height, &nrComponents, 0);
    if (data)
    {
        GLenum format;
        if (nrComponents == 1)
            format = GL_RED;
        else if (nrComponents == 3)
            format = GL_RGB;
        else if (nrComponents == 4)
            format = GL_RGBA;

        glBindTexture(GL_TEXTURE_2D, textureID);
        glTexImage2D(GL_TEXTURE_2D, 0, format, width, height, 0, format, GL_UNSIGNED_BYTE, data);
        glGenerateMipmap(GL_TEXTURE_2D);

        glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_S, GL_REPEAT);
        glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_WRAP_T, GL_REPEAT);
        glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MIN_FILTER, GL_LINEAR_MIPMAP_LINEAR);
        glTexParameteri(GL_TEXTURE_2D, GL_TEXTURE_MAG_FILTER, GL_LINEAR);

        stbi_image_free(data);
    }
    else
    {
        std::cout << "Texture failed to load at path: " << path << std::endl;
        stbi_image_free(data);
    }

    return textureID;
}

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

For future experience, I am hoping to continue to grow in my knowledge with computers by continuing my education with a Master's Degree in Cyber Security. I am also going to continue obtaining field-experience by applying as a full time investigator with the Computer Foresic Teams and this positions will allow me to attend more classes and seminars to gain additional education in the field of computers.

