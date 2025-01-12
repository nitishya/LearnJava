multithreading
```
package multiThreading;

public class User implements Runnable{
	private String userName;
	
	public User(String userName) {
		this.userName = userName;
	}
	
	public void run() {
		System.out.println("Thread started for the user: " + userName);
		try {
			for(int i=1;i<=5;i++) {
				System.out.println(userName + "is posting message" +i);
				Thread.sleep(1000);
			}
		}catch(InterruptedException e) {
			e.printStackTrace();
		}
		 System.out.println("Thread finished for user: " + userName); 
	}	
}

public class Impectus {

	public static void main(String[] args) {
		System.out.println("Main thread started");
		
		//creating runnable instances 
		User user1= new User("ALice");
		
		//creting thread using runnable 
		Thread thread1 = new Thread(user1);
		
		thread1.start();
		
		try {
			thread1.join();
		}catch(InterruptedException e) {
			e.printStackTrace();
		}

	}

}
```

snapshot problem 
```
package interview;

import java.util.ArrayList;
import java.util.List;

public class SnapshotArray {

	private List<int[]> history;
	private int[] array;
	private int snapId;
	
	public SnapshotArray(int length) {
		array = new int[length];
		history = new ArrayList<>();
		snapId = 0;
		
	}
	
	public void set(int index,int val) {
		array[index] = val;	
	}
	
	public int snap() {
		history.add(array.clone());
		return snapId++;
	}
	
	public int get(int index,int snap_id) {
		return history.get(snap_id)[index];
	}
	
	public static void main(String[] args) {	
      //the given input ;
	}

}
```


get username and the post sql command 
```
SELECT u.username,u.email,COUNT(a.post_id) AS total_posts
FROM users u
JOIN activity a
ON u.user_id = a.user_id
WHERE a.post_date >= CURRENT_DATE - INTERVAL 30 DAY
GROUP BY u.username,u.email
ORDER BY total_posts DESC
LIMIT 10;
```       

/like and /dislike 

'''
@Service
pulic class PostService{

@autowired
private PostRepository postRepository;


@autowired
private ReactionRepository reactionRepository;


//check if post valid 
public boolean isPostValid(Long postId){
return postRepository.existById(postId);
}

//get likes and dislikes using streams 


