# Reverse Linked List:
## Appraoch 1 (Iterative Method):

-   Initialize three pointers **prev** as NULL, **curr** as **head**, and **next** as NULL. 
-   Iterate through the linked list. In a loop, do the following:
    -   Before changing the **next** of **curr**, store the **next** node 
        -   next = curr -> next
    -   Now update the **next** pointer of **curr** to the **prev** 
        -   curr -> next = prev 
    -   Update **prev** as **curr** and **curr** as **next** 
        -   prev = curr 
        -   curr = next

![RGIF2](https://github.com/IshaanAdarsh/TIL/assets/100434702/625def69-85cc-4d02-84b3-f00edf9e4d18)

### CODE:
```c++
Node* reverseLinkedList(Node *head)
{
  if(head == NULL || head -> next == NULL){
    return head;
  }
  
  // Initialize current, previous and next pointers
  Node* prev = NULL;
  Node* curr = head;
  Node* forward = NULL:
  
  while(curr != NULL){
    // Store forward
    forward = curr -> next;
    //Reverse current node's pointer
    curr -> next = prev;
    //Move pointers one position ahead
    prev = curr;
    curr = forward;
  }
  
  return prev;
}
```

- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

## Approach 2 (Tail Recursive Method):
Follow the steps below to solve the problem:

-   First update next with next node of current i.e. **next = current->next**
-   Now make a reverse link from current node to previous node i.e. curr->next = prev
-   If the visited node is the last node then just make a reverse link from the current node to previous node and update head.

### CODE:

```c++
viod reverse(Node* &head, Node* curr, Node* prev)
{
    //base case
    if(curr==NULL){
        //point head to prev and return
        head = prev;
        return;
    }
    
    //Move the pointer forward
    Node* forward = curr -> next;
    
    //call the function recursively
    reverse(head,forward,curr);
    
    //Solves the current case (reverses the LL)
    curr -> next = prev;
}

Node*reverseLinkedList(Node *head)
{
    Node* curr = head;
    Node* prev = NULL;
    reverse(head,curr,prev);
    return head;
}
```

- **Time Complexity:** O(N)
- **Space Complexity:** O(N)

## Approach 3 (Recursive Method):

Follow the steps below to solve the problem:

-   Divide the list in two parts -- first node and rest of the linked list.
-   Call reverse for the rest of the linked list.
-   Link the rest linked list to first.
-   Fix head pointer to NULL

![Linked-List-Rverse](https://github.com/IshaanAdarsh/TIL/assets/100434702/cc6e605b-6aff-4641-b91f-17d6d149432f)

### CODE:

```c++
Node* reverse(Node* head)
    {
        if (head == NULL || head->next == NULL)
            return head;
 
        //reverse the rest list and put the first element at the end
        Node* rest = reverse(head->next);
        head->next->next = head;
 
        //tricky step -- see the diagram
        head->next = NULL;
 
        // fix the head pointer 
        return rest;
    }
```

- **Time Complexity:** O(N)
- **Space Complexity:** O(N)

# Reverse Linked List in 'K' group:

## Recursive Approach:
-   Reverse the first sub-list of size k. While reversing keep track of the next node and previous node. Let the pointer to the next node be *next *and pointer to the previous node be *prev*. 
-   *head->next = reverse(next, k)* ( Recursively call for rest of the list and link the two sub-lists )
-   Return *prev *( *prev *becomes the new head of the list)

![ReverseALinkedListInAGroupofGivenSize1](https://github.com/IshaanAdarsh/TIL/assets/100434702/771bcd01-9308-4b9d-9b7f-ebb650e62259)

### CODE:

```c++
Node* reverse(Node* head, int k)
{
    // base case
    if (!head)
        return NULL;
    Node* current = head;
    Node* next = NULL;
    Node* prev = NULL;
    int count = 0;
  
    // reverse first k nodes of the linked list
    while (current != NULL && count < k) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
        count++;
    }
  
    /* next is now a pointer to (k+1)th node
    Recursively call for the list starting from current.
    And make rest of the list as next of first node */
    if (next != NULL)
        head->next = reverse(next, k);
  
    /* prev is new head of the input list */
    return prev;
}
```

-   **Time Complexity:** O(N).
-   **Auxiliary Space:** O(N/k)

## Iteractive Approach (Space Optimized):

1.  Create a dummy node and point it to the head of input i.e dummy->next = head.
2.  Calculate the length of the linked list which takes O(N) time, where N is the length of the linked list.
3.  Initialize three-pointers prev, curr, next to reverse k elements for every group.
4.  Iterate over the linked lists till next!=NULL.
5.  Points curr to the prev->next and next to the curr next.
6.  Then, Using the inner for loop reverse the particular group using these four steps:

> -   curr->next = next->next
> -   next->next = prev->next
> -   prev->next = next
> -   next = curr->next

7. This for loop runs for k-1 times for all groups except the last remaining element, for the last remaining element it runs for the remaining length of the linked list -- 1.
8. Decrement count after for loop by k count -= k, to determine the length of the remaining linked list.
9. Change prev position to curr, prev = curr.

### CODE:

```c++
Node* reverse(Node* head, int k)
{
    // If head is NULL or K is 1 then return head
    if (!head || k == 1)
        return head;
  
    Node* dummy = new Node(); // creating dummy node
    dummy->data = -1;
    dummy->next = head;
  
    // Initializing three points prev, curr, next
    Node *prev = dummy, *curr = dummy, *next = dummy;
  
    // Calculating the length of linked list
    int count = 0;
    while (curr) {
        curr = curr->next;
        count++;
    }
  
    // Iterating till next is not NULL
    while (next) {
        // Curr position after every reverse group
        curr = prev->next;
        
        // Next will always next to curr
        next = curr->next;
        
        // toLoop will set to count - 1 in case of remaining element
        int toLoop = count > k ? k : count - 1;
        
        for (int i = 1; i < toLoop; i++) {
            // 4 steps as discussed above
            curr->next = next->next;
            next->next = prev->next;
            prev->next = next;
            next = curr->next;
        }
        // Setting prev to curr
        prev = curr;
        
        // Update count
        count -= k;
    }
    // dummy -> next will be our new head for output linkek list
    return dummy->next;
}
```

-   **Time Complexity:** O(N).
-   **Auxiliary Space:** O(1)
