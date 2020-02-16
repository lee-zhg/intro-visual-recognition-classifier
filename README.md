# Classify Pictures with Watson Studio & Visual Recognition

The IBM Watson™ Visual Recognition service uses deep learning algorithms to analyze images for scenes, objects, and other content. A set of built-in models provides highly accurate results without training to analyze images for objects, colors, food, explicit content and other subjects for insights into your visual content.

* General model - Default classification from thousands of classes.
* Explicit model - Whether an image is inappropriate for general use.
* Food model - Specifically for images of food items.

Watson Visual Recognition makes it easy to extract thousands of labels from your images and detect for specific content out-of-the-box. In acdition to the pre-built models, you can also build custom models to detect for specific content in images inside your applications.

In this workshop, you learn how to

* classify photos with the pre-built models
* build new classification model


## Sample Visual Recognition Use Cases

The Visual Recognition can be used for diverse applications and industries, such as:

* Manufacturing - Use images from a manufacturing setting to make sure products are being positioned correctly on an assembly line
* Visual auditing - Look for visual compliance or deterioration in a fleet of trucks, planes, or windmills out in the field, train custom models to understand what defects look like
* Insurance - Rapidly process claims by using images to classify claims into different categories


## Objectives

After completing this workshop, you should be able to:

* build a custom image classification model by using the Watson Studio and Visual Recognition
* classify photos with your custom model
* call your custom model via the Watson Visual Recognition APIs to classify photos
* classify photos with built-in models in the Watson Visual Recognition service


## Tools Used

* Watson Studio - Watson Studio is a powerful AI/Machine Learning development platform with many capabilities. It's used to create a custom visual classification model in this workshop.
* Watson Visual Recognition - Visual Recognition understands the contents of images - tag images, find human faces, approximate age and gender, and find similar images in a collection.


## Requirements

* IBM Cloud account - [sign up](https://cloud.ibm.com/registration/) if you don't have an account yet.


## Workshop Flow

The rest of this `README` provide the workshop instructions.


### Prerequisites

1. Ensure you have access to a `Waston Studio` instance and `Visual Recognition` instance. If you need to provision either instance, see the instructions in the [Setup Watson Studio & Visual Recognition document](EnvironmentSetup.md)

1. Clone this repository on your local computer.

    * If you have GIT on your machine, clone this repository locally. Open a terminal and run:

        ```
        $ git clone https://github.com/lee-zhg/intro-visual-recognition-classifier.git
        ```

    * If you do NOT have GIT on your machine, you can just download the repository as a ZIP file. In the browser window, select :

        ![Download Repo](docs/images/ss0.png)


### Setup Project in Watson Studio

1. Start Watson Studio by logging in at [https://dataplatform.ibm.com](https://dataplatform.ibm.com)

1. From the dashboard page, Click the **`Create a project`** link to create a new project in Watson Studio.

    ![Create Project](docs/images/ss8.png)

1. Select option `Select an empty project`.

1. Give your project a name and click **`Create`** on the bottom right.

    ![Name Project](docs/images/ss9.png)

1. Next you have to associate a `Visual Recognition` service to the project. 

1. Select on `Settings` tab on the top banner of the project.

1. Click the `Add Service` link under `Associate Services`.

1. Select `Watson` to add a Watson service to the project.

    ![Associate Service Settings](docs/images/settings.png)

1. Select `Visual Recognition` from the list of available Watson Services.

    ![Add Associated Service](docs/images/add-associated-service.png)

1. Select the `Existing` tab and select the name of your `Visual Recognition` service instance.

    ![Add Existing VC Service](docs/images/choose-vc-service.png)
  
1. Click `Select`.

1. The `Visual Recognition` service is now listed as one of your `Associated Services`.

    ![Associated Service](docs/images/associated-service.png)


### Classify Picture with Built-in Model

`Visual Recognition` has pre-built models. To classify picture with the out-box models,

1. Click the `Navigation Menu` (three horizental lines) at the top-left corner.

1. Select `Watson Services` under `Services`.

    ![Pre-built Model 01](docs/images/generalmodel01.png)

1. Locate your `Visual Recognition` service instance.

1. Click `Launch Tool`.

1. Click `Test` in the `General` tile.

    ![Pre-built Model 02](docs/images/generalmodel02.png)

1. Select the `Test` tab.

    ![Pre-built Model 03](docs/images/generalmodel03.png)

1. Click `browse` on the canvas with lab **Drop image files here to let the classifier analyze them or browse to select files**.

1. Select file `docs/images/test-food-fruit.png`.

1. The `General` model classifies the picture.

    ![Pre-built Model 04](docs/images/generalmodel04.png)


### Add Data Assets

To add tarining photos to the `Waston Studio` project as `data assets`, 

1. Navigate back to the  `Watson Studio` project by clicking your project link at the top-left.

    ![Data Asset 01](docs/images/datassets01.png)

1. Navigate to `Assets` tab.

    ![Data Asset 02](docs/images/datassets02.png)

1. Click `Add to project` button on the top.

1. Select `Visual Recognition` tile.

    ![Data Asset 03](docs/images/datassets03.png)

1. The `Load-Files-Catalog` window is displayed at the top-right corner.

    ![Data Asset 04](docs/images/datassets04.png)

1. Click `browse` link to upload the following files
    * data/BrooklynLager.zip
    * data/WoodchuckHardCider.zip
    * data/negative.zip

1. You have to load file one at a time. You have three data assets ready to build your custom model after you completed the loading.

    ![Data Asset 04](docs/images/datassets05.png)


### Create a Custom Visual Recognition Classification Model

To create a custom visual recognition classification model,

1. Navigate to `Assets` tab within your `Watson Studio` project.

1. Click `Add to project` button on the top.

1. Select `Visual Recognition` tile.

    ![Custom Model 01](docs/images/custommodel01.png)

1. Rename the model to `My Bottle Model`.

    ![Custom Model 02](docs/images/custommodel02.png)

1. Click `Create Model +  ` link on the `Classify Image` tile.

1. Click `Create a class` link.

    ![Custom Model 03](docs/images/custommodel03.png)

1. Enter `BrooklynLager` as the new `class label`.

    ![Custom Model 04](docs/images/custommodel04.png)

1. `Create`.

1.  Class `BrooklynLager` is added to the canvas.

    ![Custom Model 05](docs/images/custommodel05.png)

1. Drag and drop the data asset `BrooklynLager.zip` under `Add from existing project files` section on the right to the new class `BrooklynLager` on the canvas.

    ![Custom Model 06](docs/images/custommodel06.png)

1. It may take a few moment to add 25 training photos to the class `BrooklynLager`.

1. Repeat the same process for create another new class `WoodchuckHardCider` and add the data asset `WoodchuckHardCider.zip` to the new class as its corresponding training photos.

1. Class `Negative` was created by default. Add data asset `negative.zip` to  the `Negative` class.

    ![Custom Model 07](docs/images/custommodel07.png)

1. Click the `Train Model` button on tje top-right.

1. The training process may take a few minutes. After the model training is completed, message `Training successful: Your model training was successful. Click here to view and test your model.` is displayed  on the top of your window.

    ![Custom Model 08](docs/images/custommodel08.png)


### Test Custom Model

To test your custom model,

1. You may click the `here` link inm the above message to go to test and see the detail information of the custom model.

    ![Custom Model 09](docs/images/custommodel09.png)

1. Take note of `Model ID` which will be needed for the remaining of the workshop.

1. Select the `Test` tab.

1. Select or drag and drop testing image file `data/BrooklynLager-test.JPG` to the canvas.

1. The custom model classifies the image.

    ![Custom Model 10](docs/images/custommodel10.png)

1. The testing image file `data/WoodchuckHardCider-test.JPG` is also available.

1. Navigate to the `Implementation` tab. Code snippets of calling the model via APIs are provided in various programming languages.

    ![Custom Model 11](docs/images/custommodel11.png)

1. Accessing the custom model via APIs will be discussed in detail in the remaining of the workshop.


### Retrieve apikey of Visual Recognition

To retrieve `apikey` of your `Visual Recognition` service instance,

1. Navigate to the `IBM Cloud Resource List` at https://cloud.ibm.com/resources.

1. Expand `Servives` section.

1. Select your `Visual Recognition` instance.

1. Select the `Service credentials` in the left pane.

1. There should be at least one `Service Credential` defined on the right. In case there is no `Service Credential` defined, click `New credential` button and take all default to create one.

1. Click `View credential` link of any `credential` instance and expand it.

1. Take note of `apikey` property. It'll be used for the remaining of the workshop.


### Access Custom Model APIs via Curl

To call your custom model API via `Curl`,

1. Open a command window or terminal.

1. Navigate to the folder where this repo was downloaded.

    ```
    cd <PATH>/intro-visual-recognition-classifier

1. Classify an image via GET API

    ```
    curl -u "apikey:{apikey}" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?url=ttps://raw.githubusercontent.com/lee-zhg/intro-visual-recognition-classifier/master/data/BrooklynLager-test.jpg&version=2018-03-19&classifier_ids=MyBottleModel_290228105"
    ```

    > Note: Replace `{apikey}` with the `apikey` of your `Visual Recognition` instance.

    > Note: `MyBottleModel_290228105` is the custom model ID. Replace it with your custom model ID which can be found on the `Overview` tab of your custom model.

    > Note: `ttps://raw.githubusercontent.com/lee-zhg/intro-visual-recognition-classifier/master/data/BrooklynLager-test.jpg` is the testing image in the Github.

1. The REST API call returns the classification result below. With 90.7% confidence, it's classified as `BrooklynLager`.

    ```
    {
        "images": [
            {
                "classifiers": [
                    {
                        "classifier_id": "MyBottleModel_290228105",
                        "name": "My Bottle Model",
                        "classes": [
                            {
                                "class": "BrooklynLager",
                                "score": 0.907
                            }
                        ]
                    }
                ],
                "source_url": "https://raw.githubusercontent.com/lee-zhg/intro-visual-recognition-classifier/master/data/BrooklynLager-test.jpg",
                "resolved_url": "https://raw.githubusercontent.com/lee-zhg/intro-visual-recognition-classifier/master/data/BrooklynLager-test.jpg"
            }
        ],
        "images_processed": 1,
        "custom_classes": 2
    }
    ```

1. Classify an image via POST API

    ```
    curl -X POST -u "apikey:{apikey}" -F "images_file=@<PATH of your downloaded repo folder>/intro-visual-recognition-classifier/data/WoodchuckHardCider-test.jpg" -F "threshold=0.6" -F "classifier_ids=MyBottleModel_290228105" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"
    ```

    >Note: Replace `{apikey}` with the `apikey` of your `Visual Recognition` instance.

    > Note: `MyBottleModel_290228105` is the custom model ID. Replace it with your custom model ID which can be found on the `Overview` tab of your custom model.

    >Note: `<PATH of your downloaded repo folder>/intro-visual-recognition-classifier/data/WoodchuckHardCider-test.jpg` is the testing image on your local machine.

1. The REST API call returns the classification result below. With 90.8% confidence, it's classified as `WoodchuckHardCider`.

    ```
    {
        "images": [
            {
                "classifiers": [
                    {
                        "classifier_id": "MyBottleModel_290228105",
                        "name": "My Bottle Model",
                        "classes": [
                            {
                                "class": "WoodchuckHardCider",
                                "score": 0.908
                            }
                        ]
                    }
                ],
                "image": "WoodchuckHardCider-test.jpg"
            }
        ],
        "images_processed": 1,
        "custom_classes": 2
    }
    ```

1. You may combine your new custom model with the `default` Classification model that comes with your `Visual Recognition` service when classifying an image. So, you can take advantage of your custom model as well as the pre-built model. For example,

    ```
    curl -X POST -u "apikey:{apikey}" -F "images_file=@<PATH of your downloaded repo folder>/intro-visual-recognition-classifier/data/WoodchuckHardCider-test.jpg" -F "threshold=0.6" -F "classifier_ids=MyBottleModel_290228105,default" "https://gateway.watsonplatform.net/visual-recognition/api/v3/classify?version=2018-03-19"
    ```

    > Note: `classifier_ids=MyBottleModel_290228105,default` in the call specifies that you want to combine your custom model `classifier_ids=MyBottleModel_290228105` and pre-built model `default`.

    >Note, Replace `{apikey}` with the `apikey` of your `Visual Recognition` instance.

    > Note: `MyBottleModel_290228105` is the custom model ID. Replace it with your custom model ID which can be found on the `Overview` tab of your custom model.

    >Note: `<PATH of your downloaded repo folder>/intro-visual-recognition-classifier/data/WoodchuckHardCider-test.jpg` is the testing image on your local machine.

1. With combining your customer model and the pre-built model, the REST API call returns many more classification results. In addition to identifying the testing image as `WoodchuckHardCider` class, it's also classified as `soft drink`, `beverage`, `food` and etc with different confident score.

    ```
    {
        "images": [
            {
                "classifiers": [
                    {
                        "classifier_id": "MyBottleModel_290228105",
                        "name": "My Bottle Model",
                        "classes": [
                            {
                                "class": "WoodchuckHardCider",
                                "score": 0.908
                            }
                        ]
                    },
                    {
                        "classifier_id": "default",
                        "name": "default",
                        "classes": [
                            {
                                "class": "soft drink",
                                "score": 0.751
                            },
                            {
                                "class": "beverage",
                                "score": 0.842
                            },
                            {
                                "class": "food",
                                "score": 0.888
                            },
                            {
                                "class": "olive color",
                                "score": 0.776
                            },
                            {
                                "class": "claret red color",
                                "score": 0.654
                            }
                        ]
                    }
                ],
                "image": "WoodchuckHardCider-test.jpg"
            }
        ],
        "images_processed": 1,
        "custom_classes": 2
    }
    ```


### Access Custom Model APIs via Node.js

To call your custom model API in `Node.js` application,

1. Open file `app.js` in your favor file editor. File `app.js` locates  in the root folder of your downloaded repo directory.

1. Modify the following two lines.

    ```
    iam_apikey: '{iam_api_key}'
    var classifier_ids = ["MyBottleModel_290228105"];
    ```

    > Note: Replace `{apikey}` with the `apikey` of your `Visual Recognition` instance.

    > Note: Replace `MyBottleModel_290228105` with your custom model ID. It can be found on the `Overview` tab of your custom model. 
    
    > Note: To combine your custom model with the pre-built model, change the line to `var classifier_ids = ["MyBottleModel_290228105","default"];`

1. Save  the changes.

1. Download required libraries.

    ```
    npm install
    ```

1. Run the sample application.

    ```
    node app.js
    ```

1. The sample application classifies the image `BrooklynLager-test.jpg` as below.

    ```
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "MyBottleModel_290228105",
              "name": "My Bottle Model",
              "classes": [
                {
                  "class": "BrooklynLager",
                  "score": 0.907
                }
              ]
            }
          ],
          "image": "BrooklynLager-test.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 2
    }
    ```

1. When you combine the custom model with the pre-built model, the image `BrooklynLager-test.jpg` is classified as below.

    ```
    {
      "images": [
        {
          "classifiers": [
            {
              "classifier_id": "MyBottleModel_290228105",
              "name": "My Bottle Model",
              "classes": [
                {
                  "class": "BrooklynLager",
                  "score": 0.907
                }
              ]
            },
            {
              "classifier_id": "default",
              "name": "default",
              "classes": [
                {
                  "class": "steak sauce",
                  "score": 0.613,
                  "type_hierarchy": "/food/food product/food ingredient/food seasoning/condiment/steak sauce"
                },
                {
                  "class": "condiment",
                  "score": 0.672
                },
                {
                  "class": "food seasoning",
                  "score": 0.672
                },
                {
                  "class": "food ingredient",
                  "score": 0.672
                },
                {
                  "class": "food product",
                  "score": 0.673
                },
                {
                  "class": "food",
                  "score": 0.876
                },
                {
                  "class": "beverage",
                  "score": 0.795
                },
                {
                  "class": "alcoholic beverage",
                  "score": 0.684
                },
                {
                  "class": "bottle green color",
                  "score": 0.926
                },
                {
                  "class": "reddish brown color",
                  "score": 0.649
                }
              ]
            }
          ],
          "image": "BrooklynLager-test.jpg"
        }
      ],
      "images_processed": 1,
      "custom_classes": 2
    }


## Build Mobile Application with your Custom Model

Refer to the resource/repo links below to build mobile application with a custom model.

* https://cloud-annotations.github.io/training/classification/cli/

* https://cloud-annotations.github.io/training/object-detection/cli/

* https://github.com/cloud-annotations/custom-training
































