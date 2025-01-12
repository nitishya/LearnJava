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
