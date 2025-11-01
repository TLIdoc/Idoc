# This is my repository
My name is Unity
![this is img](https://unity.com/_next/image?url=https%3A%2F%2Fcdn.sanity.io%2Fimages%2Ffuvbjjlp%2Fproduction%2F6d1df49565a2ad20ffa8386f1465ba52039133e3-1920x1080.png&w=3840&q=75)
I'm Unity Game.dev. There is example of my code
                    [Header("Input Actions")]
                    public InputActionReference moveAction; // expects Vector2
                    public InputActionReference jumpAction; // expects Button

                    private void Awake()
                    {
                        controller = gameObject.AddComponent<CharacterController>();
                    }

                    private void OnEnable()
                    {
                        moveAction.action.Enable();
                        jumpAction.action.Enable();
                    }

                    private void OnDisable()
                    {
                        moveAction.action.Disable();
                        jumpAction.action.Disable();
                    }
this     ...                
* [player move..](https://docs.unity3d.com/ScriptReference/CharacterController.Move.html)
* [gun shooting](https://discussions.unity.com/t/gun-shooting-script-c/525410)
* [enemy AI](https://discussions.unity.com/t/gun-shooting-script-c/525410)