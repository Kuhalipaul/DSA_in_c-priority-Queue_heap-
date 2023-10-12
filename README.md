# DSA_in_c-priority-Queue_heap-
#include <iostream>
#include <climits>
using namespace std;

#include "solution.h"

#include <vector>

class PriorityQueue {
    vector<int> pq;

   public:
    bool isEmpty() { 
        return pq.size() == 0; 
    }

    int getSize() { 
        return pq.size(); 
    }

    int getMin() {
        if (isEmpty()) {
            return 0;
        }

        return pq[0];
    }

    void insert(int element) {
        pq.push_back(element);

        int childIndex = pq.size() - 1;

        while (childIndex > 0) {
            int parentIndex = (childIndex - 1) / 2;

            if (pq[childIndex] < pq[parentIndex]) {
                int temp = pq[childIndex];
                pq[childIndex] = pq[parentIndex];
                pq[parentIndex] = temp;
            } else {
                break;
            }

            childIndex = parentIndex;
        }
    }

    int removeMin() {
        // Write your code here

        //1st check priority Queue is empty or not
         if (isEmpty()) {
            return 0;
        }
        int ans=pq[0];
        pq[0]=pq[pq.size()-1];
        pq.pop_back();
  //Down-heapify
  int parentIndex=0;
  int leftChildIndex=2*parentIndex+1;
  int rightChildIndex=2*parentIndex+2;
while(leftChildIndex<pq.size()){
    int minIndex=parentIndex;
    if(pq[parentIndex]>pq[leftChildIndex]){
        minIndex=leftChildIndex;
    }
    if(rightChildIndex<pq.size() && pq[rightChildIndex]<pq[minIndex]){
        minIndex=rightChildIndex;
    }
      if(minIndex==parentIndex){
        break;
    }
    int temp=pq[minIndex];
    pq[minIndex]=pq[parentIndex];
    pq[parentIndex]=temp;
  
    parentIndex=minIndex;
    leftChildIndex=2*parentIndex+1;
    rightChildIndex=2*parentIndex+2;

}
return ans;
}
};
int main() {
    PriorityQueue pq;

    int choice;
    cin >> choice;

    while (choice != -1) {
        switch (choice) {
            case 1:  // insert
                int element;
                cin >> element;
                pq.insert(element);
                break;
            case 2:  // getMin
                cout << pq.getMin() << "\n";
                break;
            case 3:  // removeMax
                cout << pq.removeMin() << "\n";
                break;
            case 4:  // size
                cout << pq.getSize() << "\n";
                break;
            case 5:  // isEmpty
                cout << (pq.isEmpty() ? "true\n" : "false\n");
            default:
                return 0;
        }
        
        cin >> choice;
    }
}
