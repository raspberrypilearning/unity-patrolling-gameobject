![An animated gif showing a Car GameObject moving left and right across the Game view.](images/car-patrol.gif)

In the Inspector window for the GameObject, click **Add Component** and choose **Character Controller**. Position and size the controller so it covers the whole of your patrolling GameObject.

![The Inspector window showing the Character Controller component.](images/char-coll-dog.png)

![The Scene view showing the Dog GameObject with Character Collider highlighted around the frame of the Dog.](images/scene-coll-dog.png)

**Tip:** Press <kbd>Shift</kbd>+<kbd>F</kbd> to focus on the patrolling GameObject in the Scene view.

Click on **Add Component** and add a **Box Collider**. Adjust the Center y and Size y values so that other characters cannot walk through or climb on top of the patrolling GameObject:

![The Inspector window showing the Box Collider component with Center y and Size y properties highlighted.](images/box-collider.png)

**Tip:** You will also need to add Box Colliders to any other GameObjects that could move into the patrol area.

Click on **Add Component** and add a **New script**, then give your script a sensible name.

Double-click on your new script to open it in the code editor.

Add variables to control the patrol speed and patrol area:

--- code ---
---
language: cs
---

float patrolSpeed = 3.0f;
float minPosition = -4.0f;
float maxPosition = 4.0f;

--- /code ---

Add code to the 'Update()' method to make the patrolling GameObject move forward until it reaches the maxPosition then turn `180` degrees and move forward again until the minPosition is reached, then turn `180` degrees:

--- code ---
---
language: cs
---
    
    void Update()
    {
        CharacterController controller = GetComponent<CharacterController>();
        Vector3 forward = transform.TransformDirection(Vector3.forward);
        controller.SimpleMove(forward * patrolSpeed);

        if (transform.position.x > maxPosition)
        {
            transform.Rotate(0, 180, 0);
            transform.position = new Vector3(maxPosition, transform.position.y, transform.position.z);
        }
        else if (transform.position.x < minPosition)
        {
            transform.Rotate(0, 180, 0);
            transform.position = new Vector3(minPosition, transform.position.y, transform.position.z);
        }
    }
    
--- /code ---

Setting the `transform.position` after turning makes sure that the NPC isn't outside its patrol bounds after turning around.
