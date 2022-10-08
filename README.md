# Azure_ACR

### Step 01 : Container Registry Creation in Azure Portal<hr>
Let's go to the <b>Azure Portal</b> and create a container registry (e.g. registry name as: monir0908). <br>
Once the deployment is successful, it will provide us the following:<br>

<b>Login server:</b> monir0908.azurecr.io <br> 

We will need this `login server` later.

### Step 02 : Login to the ACR through CLI<hr>
There are several ways to authenticate with an Azure container registry, each of which is applicable to one or more registry usage scenarios.<br>
Recommended ways include:

- Individual login (Authenticate to a registry directly)
- AD Service Principal

Follow [this link](https://learn.microsoft.com/en-us/azure/container-registry/container-registry-authentication?tabs=azure-cli) to know more about `acr` authentication.<br>

I am assuming we have `azure cli` installed. If yes, then type:
```
az login
```
I am going for the first approach to login to the `acr`:
```
az acr login -n monir0908
```

To chek the list of images we have in our `acr`:
```
az acr repository list -n monir0908
```

### Step 03 : Listing Local Machine Images <hr>
To check the list of images stored in our local machine:

```
docker images
```

Now, it is displaying all the images stroed in our local machine. 
We have 5 images in our local machine. Let's pick `nginx` image for pushing it to the `acr`.


![Tagged Image](image_list_in_local_machine.PNG)


### Step 04 :  Tagging Image<hr>
It is mandatory to tag an image before pushing it to the `acr`.
To tag an image, 4 things are necessay:

- `image_id_that_we_want_to_push`
- `acr_login_server_url`
- `pushable_image_any_name`
- `pushable_image_version`


So let's copy the `IMAGE ID` of `nginx` image. In our case, it is `51086ed63d8c`.


![Tagged Image](image_id.PNG)

What we have now:<br>
- `image_id_that_we_want_to_push` : 51086ed63d8c (nginx image id)
- `acr_login_server_url`: monir0908.azurecr.io
- `pushable_image_any_name`: my-nginx (any chosen name)
- `pushable_image_version`: v1 (could have written latest)

Let's tag our `ngnix` image with the above detail:
```
docker tag 51086ed63d8c monir0908.azurecr.io/my-nginx:v1
```

Let's run the follwing command to see if `image tagging` worked:
```
docker images
```

It should display our tagged version of image with other images available:

![Tagged Image](image_tagged.PNG)



### Step 05 : Pushing Image to the ACR<hr>
To push the image to `acr`:
```
docker push monir0908.azurecr.io/my-nginx:v1
```

It will start pushing it to the `acr` and show the following when done.

![Tagged Image](pushed_to_acr.PNG)


### Step 06 : Checking Image in the ACR<hr>
Now, we can check if the image <b>(i.e. my-nginx)</b> can be found in our registry list in `acr`.
To check:

```
az acr repository list -n monir0908
```

It is showing our expected image <b>(i.e. my-nginx)</b> in the list.

![Tagged Image](cheked_repo_pushed.PNG)


Thank you!!
