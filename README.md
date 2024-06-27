Minimum number of Jumps to reach the end of an array in Java
Here, in this page we will discuss the program to find Minimum number of Jumps to reach the end of an array in Java . We are Given with an array of integers where each element represents the max number of steps that can be made forward from that element. We need to Write a code to return the minimum number of jumps to reach the end of the array (starting from the first element). If an element is 0, they cannot move through that element. If the end isn’t reachable, return -1.

Minimum number of Jumps to reach the end of an array
Algorithm :
Take the size of the array from the user and store it in variable say n.
Take n elements of the array from the user.
Create another function say minJumps() that will return the desired output.
Inside that minJumps(), Make a jumps[] array from left to right such that jumps[i] indicate the minimum number of jumps needed to reach arr[i] from arr[0].
To fill the jumps array run a nested loop inner loop counter is j and outer loop count is i.
Outer loop from 1 to n-1 and inner loop from 0 to i.
if i is less than j + arr[j] then set jumps[i] to minimum of jumps[i] and jumps[j] + 1. initially set jump[i] to INT MAX
Finally, return jumps[n-1].
 

Example :

Input: arr[] = {1, 3, 5, 8, 9, 2, 6, 7, 6, 8, 9}
Output: 3 (1-> 3 -> 9 -> 9)
Explanation: Jump from 1st element to 2nd element as there is only 1 step, now there are three options 5, 8 or 9. If 8 or 9 is chosen then the end node 9 can be reached. So 3 jumps are made.

Minimum number of jumps to reach the end of an array
Minimum number of jumps to reach the end of an array
Code in Java
Run
public
class Main {
    private
    static int minJumps(int[] arr, int n) {
        // jumps[n-1] will hold the
        int jumps[] = new int[n];

        int i, j;
        // if first element is 0,
        if (n == 0 || arr[0] == 0) return Integer.MAX_VALUE;

        // end cannot be reached
        jumps[0] = 0;
        // Find the minimum number of jumps to reach arr[i]
        // from arr[0], and assign this value to jumps[i]

        for (i = 1; i < n; i++) {
            jumps[i] = Integer.MAX_VALUE;

            for (j = 0; j < i; j++) {
                if (i <= j + arr[j] && jumps[j] != Integer.MAX_VALUE) {
                    jumps[i] = Math.min(jumps[i], jumps[j] + 1);
                    break;
                }
            }
        }
        return jumps[n - 1];
    }

    // driver program to test above function
    public
    static void main(String[] args) {
        int arr[] = {2, 1, 3, 2, 3, 4, 5, 1, 2, 8};

        System.out.println("Minimum number of jumps to reach end is : " +
                           minJumps(arr, arr.length));
    }
}
Output
Minimum number of jumps to reach end is : 3
Related Pages
Given an array which consists of only 0, 1 and 2

Move all the negative elements to one side of the array

Find the Union and Intersection of the two sorted arrays

Find Largest sum contiguous Subarray

Minimize the maximum difference between heights 

Method 2
Run
import java.util.*;
public
class Main {
    public
    static int minJumps(int[] arr) {
        int i = 0, jump = 0, n = arr.length;
        while (i < n - 1) {
            int val = arr[i];
            if (val == 0) {
                return -1;
            }
            int max = 0, maxInd = -1;
            if ((i + val) >= (n - 1)) {
                return jump + 1;
            }
            for (int j = i + 1; j < n && j <= (i + val); j++) {
                if ((j + arr[j]) > max) {
                    max = j + arr[j];
                    maxInd = j;
                }
            }
            i = maxInd;
            jump++;
        }
        return jump;
    }
    public
    static void main(String[] args) throws Exception {
        Scanner sc = new Scanner(System.in);
        int n = 5;
        int[] arr = {1,2,4,5,6};
        System.out.print("Minimum number of Jumps to reach the end of an array= ");
        int ans = minJumps(arr);
        System.out.println(ans);
    }
}
Output
5
1 2 4 5 6
3
Prime Course Trailer

Related Banners
Get PrepInsta Prime & get Access to all 200+ courses offered by PrepInsta in One Subscription

Get Prime
Login/Signup to comment


Prithuraj
int arr[] = { 2, 1, 3, 2, 3, 4, 5, 1, 2, 8 };
int ptr = 0;
int destination = 0;
int jump = 0;
for (int i = 0; i < arr.length; i++) {
destination = Math.max(destination, arr[i] + i);
if (ptr == i && destination < arr.length) {
ptr = destination;
jump++;
}
}
System.out.println(jump);
