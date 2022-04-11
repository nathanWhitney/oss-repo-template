Checkpoint 1:

![image](https://user-images.githubusercontent.com/68211239/162488779-fb0dc513-6f5a-478e-80db-7d05e65ea6ec.png)

Checkpoint 2:

![image](https://user-images.githubusercontent.com/68211239/162760384-141121fb-5d3f-42db-a542-04fb75f474c4.png)

![image](https://user-images.githubusercontent.com/68211239/162493892-1de52d8c-3fd9-4468-bd75-ca4b01a12a21.png)

![image](https://user-images.githubusercontent.com/68211239/162760486-92157b2e-f6a2-467a-840c-f74d45c04f45.png)

![image](https://user-images.githubusercontent.com/68211239/162760619-8e024d91-2321-4c47-8c11-9be5b4fe58cc.png)

![image](https://user-images.githubusercontent.com/68211239/162761619-bb55dd5e-1b33-48a4-a6a1-b7c0eb0ae81d.png)



Checkpoint 3:

![bag](https://user-images.githubusercontent.com/68211239/162672260-7e343b65-4d3c-41b6-a22a-0d7899df6ffc.JPG)

![pants](https://user-images.githubusercontent.com/68211239/162672229-60f6c3f0-c2df-4e98-8fa3-e2e4e5087daf.JPG)

![shirt](https://user-images.githubusercontent.com/68211239/162672163-6f50c2a0-d535-4d4b-ab91-36dfd9dbfe0d.JPG)

![shoes](https://user-images.githubusercontent.com/68211239/162760997-bc3960bd-b5cf-428c-904b-c7c030433a30.JPG)


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
```{r}
holding = np.array([[bag_np], [pants_np],[shirt_np],[shoes_np]])
labels = [8, 1, 0, 7]
holding = 1-holding
holding.resize(4,28,28)

predictions = probability_model.predict(holding)

for i in range(4):
    plt.figure(figsize=(6,3))
    plt.subplot(1,2,1)
    plot_image(i, predictions[i], labels, holding)
    plt.subplot(1,2,2)
    plot_value_array(i, predictions[i],  labels)
    plt.show()
```
Two runs

![image](https://user-images.githubusercontent.com/68211239/162671860-b5a03b26-db47-46a9-9408-ba6156dff05c.png)

The confusion with sandals is likely caused by the white bottom of the sneaker. While the other is likely just because of the high amount of general confusion caused by the high amount of grey in the image.

![image](https://user-images.githubusercontent.com/68211239/162762343-86b32c7f-124a-4eab-bede-690578008e18.png)

Flipping the image of the first shows that the direction of the shoe caused an error in logic in some rotations (it does still see it as a sandle when that error is not occuring)



