package minheap;

import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

/**
 *
 * @author alexbrodsky
 */

public class MinHeap {
    
    private int array[];
    private int arraySize; // max array size, CAPACITY
    private int heapSize; // current heap size, set to 0
    // init method

    public MinHeap(int arraySize) {
        this.arraySize = arraySize;
        this.array = new int[arraySize];
        this.heapSize = 0;
    }
    
    // Private Class methods
    
    //parent (i-1)/ 3
    //child1 (3*i + 1)
    //child2 (3*i + 2)
    //child3 (3*i + 3)
    
    private void floatUp(int array[], int child) {
        int parent = (child - 1) / 3;
        if (child == 0) { //child is the root, has no parents
            return;
        }
        if (array[child] < array[parent]) {
            swap(child, parent);
            floatUp(array, parent); //continue floating up        
        }
    }

    private void sinkDown(int array[], int root, int bottom) {
        int leftChild, midChild, rightChild;
        leftChild = root * 3 + 1;
        midChild = root * 3 + 2;
        rightChild = root * 3 + 3;

        int smallest = root;
        
        if (leftChild >= bottom) { //out of bounds
            return;
        }
        else if (midChild < bottom && array[leftChild] > array[midChild]) {
            leftChild = midChild; // we know left child is the smaller child
        }
        else if (rightChild < bottom && array[leftChild] > array[rightChild]) {
            leftChild = rightChild; // we know left child is the smaller child
        }
        
        if (array[root] <= array[leftChild]) {
            return;
        }
        swap(root, leftChild);
        sinkDown(array, leftChild, bottom);
           
    }
    
    private void swap (int i, int j) {
        int temp;
        temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
  
    public void insert(int element) {
        if (heapSize < arraySize) {        // check if the heap is full
            array[heapSize] = element; 
            floatUp(array, heapSize);
            heapSize++; //increase size of heap
        } 
        else {
            throw new IllegalArgumentException("Heap is full");
        }
    }
    
    public void decreaseKey(int index, int newElement) {
        // decrese the key at index to new Element's index, given that the new key is <= to the current key at index
        if (newElement <= array[index]) {
            array[index] = newElement; // need index to point to the index of the newElement
            floatUp(array, index);  // then float up new Element to correct position
        }
        else {
            throw new IllegalArgumentException("New key is greater than current key.");

        }
    
    }
    
    public int extractMin(){
        if (heapSize == 0) {// check if heap is empty first
            throw new IllegalStateException("Heap is empty");
        }
        int min = array[0]; //min is the first element in the array
        swap(0, heapSize-1); //swap position 0, the root, to the back
        heapSize--; // shrink heapSize to extract the min
        swap(0, heapSize-1); //swap position 0, the root, to the back
        //sinkDown(array, 0, heapSize-1); this was the original
        sinkDown(array, 0, heapSize);

        return min;
    }
    
    public static void main(String[] args) throws FileNotFoundException {
        String input  = "11 # Total number of instructions\n" +
                        "IN 10 # [10]\n" +
                        "IN 15 # [10 , 15]\n" +
                        "IN 27 # [10 , 15 , 27]\n" +
                        "EM # [15 , 27]\n" +
                        "IN 13 # [13 , 27 , 15]\n" +
                        "IN 11 # [11 , 27 , 15 , 13]\n" +
                        "IN 5 # [5 , 11 , 15 , 13 , 27]\n" +
                        "IN 6 # [5 , 6, 15 , 13 , 27 , 11]\n" +
                        "DK 5 4 # Decrease Key of the element at array position 5 to value 4. [4 , 5, 15 , 13 , 27 , 6]\n" +
                        "IN 3 # [3 , 4, 15 , 13 , 27 , 6 , 5]\n" +
                        "EM # Last EM operation";
        
        //File file = new File("/Users/AlexBrodsky/Desktop/CSC 3102/Heap Input Files/inputFile.txt");
        //File file = new File("/Users/AlexBrodsky/Desktop/inputFile.txt");
        //File file = new File("inputFile.txt");
        Scanner scanner = new Scanner(input);
        MinHeap heap = new MinHeap(100);
        
        int lastEM = 0; 
        
        while (scanner.hasNextLine()) {
            String line = scanner.nextLine();
            String instructions[] = line.split(" ");
            
            if (instructions[0].equalsIgnoreCase("IN")) {
                int element = Integer.parseInt(instructions[1]);
                //System.out.println(element);
                heap.insert(element);  
            }
            else if (instructions[0].equalsIgnoreCase("DK")) {
                int index = Integer.parseInt(instructions[1]);
                int newElement = Integer.parseInt(instructions[2]);
                heap.decreaseKey(index, newElement);
            } 
            else if (instructions[0].equalsIgnoreCase("EM")) {
                //heap.extractMin();
                lastEM = heap.extractMin();
            } 
        }
        if (lastEM != 0) {
                //System.out.printf("%d # Printing the result of last EM operation\n", lastEM);
                System.out.println(lastEM);

            } 
        else {
                System.out.println("No EM operations were performed.");
            }
        StringBuilder result = new StringBuilder("[");
        for (int i = 0; i < heap.heapSize; i++) {
            result.append(heap.array[i]);
            if (i < heap.heapSize-1) {
                result.append(", ");
            }
        }
        result.append("]");
        String bigResult = result.toString();
        //System.out.println(bigResult);

	scanner.close();
    }
}
