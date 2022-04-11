Checkpoint 1:

![image](https://user-images.githubusercontent.com/68211239/162488779-fb0dc513-6f5a-478e-80db-7d05e65ea6ec.png)

Checkpoint 2:

![image](https://user-images.githubusercontent.com/68211239/162493892-1de52d8c-3fd9-4468-bd75-ca4b01a12a21.png)

Checkpoint 3:

```{r}
bag = Image.open("bag.JPG")
bag_np = np.array(bag)
bag_size = bag_np.shape
new_size = (800, 800)
new_im = Image.new("RGB", new_size, (255, 255, 255))
new_im.paste(bag, ((new_size[0]-bag_size[0])//2,
                      (new_size[1]-bag_size[1])//2))
new_im = new_im.resize((28, 28))
bag_np = np.array(new_im)
bag_np = bag_np[:,:,0]
bag_np = bag_np/ 255.0
plt.imshow(bag_np)

pants = Image.open("pants.JPG")
pants_np = np.array(pants)
pants_size = (242, 301)
new_size = (360, 360)
new_im2 = Image.new("RGB", new_size, (255, 255, 255))
new_im2.paste(pants, ((new_size[0]-pants_size[0])//2,
                      (new_size[1]-pants_size[1])//2))
new_im2 = new_im2.resize((28, 28))
pants_np = np.array(new_im2)
pants_np = pants_np[:,:,0]
pants_np = pants_np/ 255.0
plt.imshow(pants_np)

shirt = Image.open("shirt.JPG")
shirt_np = np.array(shirt)
shirt_size = shirt_np.shape
new_size = (415, 415)
new_im3 = Image.new("RGB", new_size, (255, 255, 255))
new_im3.paste(shirt, ((new_size[0]-shirt_size[0])//2,
                      (new_size[1]-shirt_size[1])//2))
new_im3 = new_im3.resize((28, 28))
shirt_np = np.array(new_im3)
shirt_np = shirt_np[:,:,0]
shirt_np = shirt_np/ 255.0
plt.imshow(shirt_np)


shoes = Image.open("shoes.JPG")
shoes_np = np.array(shoes)
shoes_size = shoes_np.shape
new_size = (360, 350)
new_im4 = Image.new("RGB", new_size, (255, 255, 255))
new_im4.paste(shoes, ((new_size[0]-shoes_size[0])//2,
                      (new_size[1]-shoes_size[1])//2))
new_im4 = new_im4.resize((28, 28))
shoes_np = np.array(new_im4)
shoes_np = shoes_np[:,:,0]
shoes_np = shoes_np/ 255.0
plt.imshow(shoes_np)
```

![image](https://user-images.githubusercontent.com/68211239/162671860-b5a03b26-db47-46a9-9408-ba6156dff05c.png)


