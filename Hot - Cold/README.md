

##  Hot -Cold Game :

A game in which the player is at some place in a maze castel, and there is a key at another point and the player has to reach the key by sound clues.

**Created by:**

[Odelia Hochman](https://github.com/OdeliaHochman)

[Netanel Davidov](https://github.com/netanel208)


**Link to itch.io:**   [ Hot - Cold Game](https://odeliamos0.itch.io/hot-cold-game)


## Player :
The animation and shape of our player we downloaded from the site mentioned *below* (mixamo). We took the animations of the object and created an Animator that links and manages the transition between each animation and animation.

The player has an option to move forward, backward, right, left. 
The moving is done using the arrow keys and doing so activates the animation that matches the movement.

- `up key` - moves the player forward.
- `down key` - moves the player backward.
- `right key` - moves the player right.
- `left key` - moves the player left.

The following code shows the invocation of the coroutine function that changes the player's move mode from standing(animation "standing") to walking ("walking" animation) animation according to the keys of the keyboard keys:
```C#
        float translation = Input.GetAxis("Vertical") * speed;
        float rotation = Input.GetAxis("Horizontal") * rotationSpeed;
        translation *= Time.deltaTime;
        rotation *= Time.deltaTime;
        transform.Translate(0, 0, translation);
        transform.Rotate(0, rotation, 0);

        if (Input.GetKey(KeyCode.LeftArrow) || Input.GetKey(KeyCode.RightArrow) || Input.GetKey(KeyCode.DownArrow) || Input.GetKey(KeyCode.UpArrow))
        {
            StartCoroutine(GoToWalkMode());
            
        }
```

When the function is called we need to switch from "standing" animation to "walking" animation so we have to stop the "standing" animation and run the "walking" animation:
```C#
    IEnumerator GoToWalkMode()
    {
        animator.SetBool("stand", false);
        animator.SetBool("walking", true);
        yield return new WaitForSeconds(duration);
        // If the key is still pressed, the animation of the "walk" should continue, otherwise we will switch back from the "walk" animation to "standing" animation
        if (!Input.GetKey(KeyCode.LeftArrow) && !Input.GetKey(KeyCode.RightArrow) && !Input.GetKey(KeyCode.DownArrow) && !Input.GetKey(KeyCode.UpArrow))
        {
            animator.SetBool("walking", false);
            animator.SetBool("stand", true);
        }
    }
```


## The Maze :
We have added to all the objects that build the maze to the **Collider** and **Rigidbody** components so that the player does not fall through them.
We have defined the entire maze structure based and **duplicated** from several main game objects:

Basic Room - Contains 3 walls, floor, roof, library, lamps and candles.

Corridor - Contains 2 walls, floor, roof, library, lamps and candles.

Junction - contains only one wall, floor, roof and lamps.

So it was actually **easy** for us to build the game world and contribute a lot to the player experience.
Example:
![image](https://user-images.githubusercontent.com/44946807/81854227-48df0680-9566-11ea-9e83-84d67301f1f7.png)


## The voice
We created Audio source for a key object and configured it as follows:
Being played in loops, played in a three-dimensional area, and changing the hearing range to a radius of up to 180 from the point, we have defined that as the player moves away from the area, the sound becomes louder and as the noise approaches exponentially:

![image](https://user-images.githubusercontent.com/44946807/81856432-77aaac00-9569-11ea-8004-be76eb1a42d5.png)

## The starting position(some place in the maze):

![image](https://user-images.githubusercontent.com/45036697/81815001-229f7380-9532-11ea-8d16-3345a58d1005.png)



## The room with the key:

![image](https://user-images.githubusercontent.com/45036697/81815194-5e3a3d80-9532-11ea-8841-03dd09f3298b.png)



![image](https://user-images.githubusercontent.com/45036697/81815330-82961a00-9532-11ea-8fde-9bec88c588e2.png)



## MiniMap:

We created a MiniMap that shows the player its location in the maze.

![image](https://user-images.githubusercontent.com/45036697/81824378-15888180-953e-11ea-9497-1d530391dea4.png)




## Assets was taken from:

* Unity Asset Store:

   Medieval Room - https://assetstore.unity.com/packages/3d/environments/free-medieval-room-131004
   

* player and animated character:
 
  Mixamo - https://www.mixamo.com/#/?page=1&type=Character

* Audio - YouTube:
  
  Dead Space Audio - PA Whispers - https://www.youtube.com/watch?v=m2ZI2ACd5XQ
