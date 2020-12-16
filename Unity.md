### Spawn at timed intervals

```
  void Start()
    {
        InvokeRepeating("SpawnRandomAnimal", startDelay, spawnInterval);
    }
    
  void SpawnRandomAnimal()
    {
        int animalIndex = Random.Range(0, animalPrefabs.Length);

        Vector3 spawnLocation = new Vector3(Random.Range(-xSpawnPos, xSpawnPos), 0, zSpawnPos);

        Instantiate(animalPrefabs[animalIndex], spawnLocation, animalPrefabs[animalIndex].transform.rotation);
    }
 ```
### Collisions:
- Add collider to all objects
- Add ridgidbody to necessary objects
- Add script to all the objects

```
  private void OnTriggerEnter(Collider other)
    {
        Destroy(this.gameObject);
        Destroy(other);
    }
 ```
 
### Movement:

#### Non physics based movement
##### Move left:
```
  transform.Translate(Vector3.left * Time.deltaTime * speed);
```

### Destroy off screen objects 

```using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class DestroyOutOfBounds : MonoBehaviour
{

    public float topBound = 30.0f;
    public float lowerBound = -10.0f;

    // Start is called before the first frame update
    void Start()
    {

    }

    // Update is called once per frame
    void Update()
    {
        if (transform.position.z > topBound)
        {
            Destroy(this.gameObject);

        }
        else if (transform.position.z < lowerBound)
        {
            Debug.Log("Game Over");
            Destroy(this.gameObject);
        }

    }
}
```

### Stop key spamming

```
public class PlayerControllerX : MonoBehaviour
{
    public GameObject dogPrefab;
    private float timer = 0.0f;
    private float coolDownTime = 1.0f;
    private bool spaceBarCandBePressed = true;

    // Update is called once per frame
    private void Awake()
    {
        Time.timeScale = 1.0f;
    }

    void Update()
    {

        timer += Time.deltaTime;

        //If its been `coolDownTime` since last time space bar was pressed
        if (timer > coolDownTime)
        {
            spaceBarCandBePressed = true;
            timer = timer - coolDownTime;
        }

        if (Input.GetKeyDown(KeyCode.Space) && spaceBarCandBePressed == true)
        {
            Instantiate(dogPrefab, transform.position, dogPrefab.transform.rotation);
            spaceBarCandBePressed = false;
        }

    }
}
```
