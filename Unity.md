### Spawn at timed intervals

`InvokeRepeating("SpawnRandomAnimal", startDelay, spawnInterval);`
```
  void SpawnRandomAnimal()
    {
        int animalIndex = Random.Range(0, animalPrefabs.Length);

        Vector3 spawnLocation = new Vector3(Random.Range(-xSpawnPos, xSpawnPos), 0, zSpawnPos);

        Instantiate(animalPrefabs[animalIndex], spawnLocation, animalPrefabs[animalIndex].transform.rotation);
    }
 ```
### Collisions:
Add collider to all objects
Add ridgidbody to necessary objects

```
  private void OnTriggerEnter(Collider other)
    {
        Destroy(this.gameObject);
        Destroy(other);
    }
 ```
