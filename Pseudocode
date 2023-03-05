# CSN-232-Starve-free-Readers-Writers-Problem

## Explanation

Each semaphore(counting semaphores are used) would have two variables/data structures associated with it, namely a process queue consisting of processes waiting on that semaphore, and a value indicating the current value of the semaphore. "readCount" indicates the number of readers currently reading.

**Initially, the state is as follows:**

All process queues of the semaphores are empty.
```cpp
in->value=1;

mutex->value=1;

read->value=1;

readCount=0;
```

"mutex" is the semaphore which is needed to gain permission to access the critical section by either readers or writers. It ensures mutual exclusion.

"in" is the semaphore which is needed to prevent starvation. 


### Working:
Suppose multiple readers are reading and a writer wants to write, then the writer would call wait(in) and thereafter, no other reader would be able to enter the critical
section other than the ones already reading.

Once readCount becomes 0 i.e. all the readers who were reading finish reading, signal(mutex) would be called and thus, the writer would gain permission to write to the 
critical section.

Any reader wanting to read will then wait until the writer has finished writing.
Even if there are multiple writers, the waiting queue for semaphore "in" would just have the processes in the order they requested to access the critical section and thus, starvation is prevented as the processes would get access to the critical section in the order they requested.


## Semaphore Operations
```cpp
wait(semaphore* s){
  s->value--;
  if(s->value<0){
    //push the process on list of processes waiting on 
    //semaphore s
    block(process);
  }
}

signal(semaphore* s){
  s->value++;
  if(s->value<=0){
    //take a process out of the process list of semaphore s
    wakeup(process);
  }
}
```

## Writer Process Code
```cpp
  wait(in);
  wait(mutex);
  
  //perform writing
  
  signal(mutex);
  signal(in);

```



## Reader Process Code

```cpp
  wait(in);
  wait(read);
  readCount++;
  if(readCount==1)wait(mutex);
  signal(read);
  signal(in);
  
  //perform reading
  
  wait(read);
  readCount--;
  if(readCount==0)signal(mutex);
  signal(read);
```
