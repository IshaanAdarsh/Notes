# Linked List:
- Dynamic Data structure which is a collection of Nodes
### Advantages: 
  - Grow/Shrink at runtime
  - No Memory Wastage 
  - Easy Insterion and Delection (No shifting)

# Singly Linked List:
  - Node = DATA + NEXT NODE ADDRESS (Pointer of Node type)

![Singlelinkedlist](https://github.com/IshaanAdarsh/TIL/assets/100434702/f39c6e67-b980-43ae-8e75-d298637a2bb2)

```c++
class Node {

    public:
    int data;
    Node* next;

    //constructor
    Node(int data) {
        this -> data = data; //Data in the SLL
        this -> next = NULL; //Points to Null
    }

    //destructor
    ~Node() {
        int value = this -> data;
        //memory free
        if(this->next != NULL) {
            delete next;
            this->next = NULL;
        }
        cout << " memory is free for node with data " << value << endl;
    }

};
```
## Print the Linked List:

Print the LL by simple linear Traversal

```c++
void print(Node* &head) {
    if(head == NULL) {
        cout << "List is empty "<< endl;
        return ;
    }
    
    Node* temp = head;
    while(temp != NULL ) {
        cout << temp -> data << " ";
        temp = temp -> next;
    }
    cout << endl;
}
```

## InsertAtHead:

Adding a new node behine the ending node

![Linkedlist_insert_at_start](https://github.com/IshaanAdarsh/TIL/assets/100434702/afbfc64e-aec9-4d6c-a0ee-c2d63072d171)

```c++
// Given a reference (pointer to pointer) to the head of a list and an int, inserts a new node on the front of the list.
void InsertAtHead(Node** head_ref, int new_data)
{
	//allocate node
	Node* new_node = new Node();

	//put in the data
	new_node->data = new_data;

	//Make next of new node as head
	new_node->next = (*head_ref);

	//Move the head to point to the new node (first node )
	(*head_ref) = new_node;
}
```
-   **Time Complexity:** O(1)
-   **Auxiliary Space:** O(1)

## InsertAtTail:
Adding a new node ahead of the ending node

```c++
void insertAtTail(Node* &tail, int d) {
    //new node create
    Node* new_node = new Node(d);
    
    //make next of tail as new node
    tail -> next = new_node;
    
    //tail points to last node always
    tail  = new_node; // tail = tail -> next;
}
```
-   **Time Complexity:** O(1)
-   **Auxiliary Space:** O(1)

## InsertAtPosition:
Adding a new node at nth positon
- We need to insert node a (n-1) positon in tail fashion

![insertion-in-singly-linked-list-after-specified-node](https://github.com/IshaanAdarsh/TIL/assets/100434702/a50ff46c-c2da-4c8e-afe0-a81b448d2f39)

```c++
void insertAtPosition(Node* &tail, Node* & head, int position, int d) {

    //insert at Start
    if(position == 1) {
        insertAtHead(head, d);
        return;
    }
    
    Node* temp  = head;
    int cnt = 1;
    
    //Moves the pointer temp to (n-1)th position
    while(cnt < position-1) {
        temp = temp->next;
        cnt++;
    }

    //inserting at Last Position &to make tail point at end
    if(temp -> next == NULL) {
        insertAtTail(tail,d);
        return ;
    }

    //creating a node for d
    Node* nodeToInsert = new Node(d);

    //The address in nodeToInsert will point to original nth Position
    nodeToInsert -> next = temp -> next;
    
    //The (n-1)th position will point to temp
    temp -> next = nodeToInsert;
}
```
-   **Time Complexity:** O(N)
-   **Auxiliary Space:** O(1)

## Append (Add a node at the end):

![Linkedlist_insert_last](https://github.com/IshaanAdarsh/TIL/assets/100434702/8fdd16dc-5d69-4ff2-a0a0-42a145ff673e)

```c++
// Given a reference (pointer to pointer) to the head of a list and an int, appends a new node at the end
void append(Node** head_ref, int new_data)
{
	
	//allocate node
	Node* new_node = new Node();
	
	//Used in While loop
	Node *last = *head_ref;
	
	//Put in the data
	new_node->data = new_data;
	
	//This new node is going to be the last node, so make next of it as NULL
	new_node->next = NULL;
	
	//If the Linked List is empty,then make the new node as head
	if (*head_ref == NULL)
	{
		*head_ref = new_node;
		return;
	}
	
	//Else traverse till the last node
	while (last->next != NULL)
	{
		last = last->next;
	}
	
	//Change the next of last node
	last->next = new_node;
	return;
}
```
-   **Time complexity:** O(N)
    -   This method can also be optimized to work in O(1) by keeping an extra pointer to the tail of the linked list/
-   **Auxiliary Space:** O(1)

## DeleteNode:

Deleting a new node at nth positon

```c++
void deleteNode(int position, Node* & head) { 

    //deleting first or start node
    if(position == 1) {
        Node* temp = head;
        head = head -> next;
        //memory free start node
        temp -> next = NULL;  //Need to point the node to NULL for destructor call
        delete temp;
    }
    else
    {
        //deleting any middle node or last node
        Node* curr = head;
        Node* prev = NULL;

        int cnt = 1;
        while(cnt < position) {
            prev = curr;
            curr = curr -> next;
            cnt++;
        }

        prev -> next = curr -> next;
        curr -> next  = NULL; //Need to point the node to NULL for destructor call
        delete curr;

    }
}
```
-   **Time complexity:** O(N)
-   **Auxiliary Space:** O(1)

# Middle of Linked List:

## Approach 1(Regular Solution): 
- Traverse the whole linked list and count the no. of nodes. 
- Now traverse the list again till count/2 and return the node at count/2. 

### CODE: 

```c++
int getlength(Node* head){
  int len = 0;
  while(head != NULL){
    len++;
    head = head -> next;
  }
  
  return len;
}

Node *findMiddle(Node* head){
  int len = getlength(head);
  
  // Position of Middle Node
  int pos = (len/2)+1;
  
  //for returning middle node pointer
  Node *temp = head;
  int cnt =0;
  while(cnt<(ans-1)){
    temp = temp -> next;
    cnt++;
  }
  
  return temp;
}
```

- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

## Approach 2(Optimized Solution):
- Traverse linked list using two-pointers. Move one pointer by one and the other pointers by two. 
- When the fast pointer reaches the end, the slow pointer will reach the middle of the linked list.

![middle-of-a-given-linked-list-in-C-and-Java1](https://github.com/IshaanAdarsh/TIL/assets/100434702/6b20a15e-e8e8-4250-a626-087fc4010162)

### CODE:

```c++
Node *findMiddle(Node* head){
  if(head == NULL || hea -> next == NULL)
    return head;
  
  //2 node - needed or not ?
  if(head -> next -> next == NULL){
    return head ->next;
  }
  
  Node* slow = head;
  Node* fast = head ->next;
  
  while(fast != NULL){
    fast = fast -> next;
    if(fast != NULL){
      fast = fast ->next;
    }
    
    slow = slow ->next;
  }
  
  return slow;
}
```

### OR (Smaller Code)

```c++
    ListNode* middleNode(ListNode* head) {
        ListNode *slow = head, *fast = head;
        while (fast && fast->next){
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
```

- **Time Complexity:** O(N)
- **Space Complexity:** O(1)

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
