import heapq
import os
class BinaryTree:
    def __init__(self,value,frequ):
        self.value = value
        self.frequ = frequ
        self.left = None
        self.right = None
        
    def __lt__(self,other):
        return self.frequ < other.frequ
    
    def _eq_(self,other):
        return self.frequ == other.frequ        

class Huffmancode:
     
    def __init__(self,path):
        self.path = path
        self.__heap = []
        self.__code = {}
        self.__reversecode = {}
        
    def __frequency_from_text(self,text):
        frequ_dict = {}
        for char in text:
            if char not in frequ_dict:
                frequ_dict[char] = 0
            frequ_dict[char] += 1
        return frequ_dict    
    
    def __Build_heap(self,frequency_dict):
        for key in frequency_dict:
            frequency = frequency_dict[key]
            binary_tree_node = BinaryTree(key,frequency)
            heapq.heappush(self.__heap , binary_tree_node)
    
    def __Build_Binary_Tree(self):
        while len(self.__heap) > 1:
            binary_tree_node_1 = heapq.heappop(self.__heap)
            binary_tree_node_2 = heapq.heappop(self.__heap)
            sum_of_freq = binary_tree_node_1.frequ + binary_tree_node_2.frequ
            newnode = BinaryTree(None,sum_of_freq)
            newnode.left = binary_tree_node_1
            newnode.right = binary_tree_node_2
            heapq.heappush(self.__heap,newnode)
        return
    def __Build_Tree_Code_Helper(self,root,curr_bits):
        if root is None:
            return
        if root.value is not None:
            self.__code[root.value] = curr_bits
            self.__reversecode[curr_bits] = root.value
            return
        self.__Build_Tree_Code_Helper(root.left,curr_bits+'0')
        self.__Build_Tree_Code_Helper(root.right,curr_bits+'1')
    
    def __Build_Tree_Code(self):
        root = heapq.heappop(self.__heap)
        self.__Build_Tree_Code_Helper(root,'')
        

    def __Build_Encoded_Text(self,text):
        encoded_text = ''
        for char in text:
            encoded_text += self.__code[char]
            
        return encoded_text  
    
    
    def __Build_Padded_Text(self,encoded_text):
        padding_value = 8 - (len(encoded_text) % 8)
        for i in range(padding_value):
            encoded_text += '0'
            
        padded_info = "{0:08b}".format(padding_value)
        padded_encoded_text = padded_info + encoded_text
        return padded_encoded_text
    
    def __Build_Byte_Array(self, padded_text):
        array = []
        for i in range(0,len(padded_text) , 8):
            byte = padded_text[i:i+8]
            array.append(int(byte,2))
        return array    
    
    def compression(self):
        
        #To access the file and extract text from that file.
        filename,file_extension = os.path.splitext(self.path)
        output_path = filename + '.bin'
        with open (self.path,'r+') as file , open(output_path,'wb') as output:
            text = file.read()
            text = text.rstrip()
            
            frequency_dict = self.__frequency_from_text(text)

            #Calculate frequency of each text and store it in freq. dictionary

            build_heap = self.__Build_heap(frequency_dict)

            # Min heap for two minimum frquency.

            #Construct binary tree from Heap .

            self.__Build_Binary_Tree()

            #construct code from binary tree and stored it in dictionary.

            self.__Build_Tree_Code()

            #Construct encoded text.

            encoded_text = self.__Build_Encoded_Text(text)

            #padding of text

            padded_text = self.__Build_Padded_Text(encoded_text)

            #We have to return that binary file as an output.

            bytes_array = self.__Build_Byte_Array(padded_text)

            final_bytes = bytes(bytes_array)
            output.write(final_bytes)
        print("The file is compressed!!!")
        return output_path
    
    def __Remove_Padding(self,text):
        padded_info = text[:8]
        extra_padding = int(padded_info,2)
        text = text[8:]
        padding_removed_text = text[:-1*extra_padding]
        return padding_removed_text
        
    def __Decompress_Text(self,text):    
        decoded_text = ''
        current_bits = ''
        for bit in text:
            current_bits += bit
            if current_bits in self.__reversecode:
                character = self.__reversecode[current_bits]
                decoded_text += character
                current_bits = ""
        return decoded_text
    
    
    def decompress(self,input_path):
        filename,file_extension = os.path.splitext(input_path)
        output_path = filename + '_decompressed' + '.txt'
        with open(input_path,'rb') as file , open(output_path,'w') as output:
            bit_string = ''
            byte = file.read(1)
            while byte:
                byte = ord(byte)
                bits = bin(byte)[2:].rjust(8,'0')
                bit_string += bits
                byte = file.read(1)
                
            actual_text = self.__Remove_Padding(bit_string)    
            decompressed_text = self.__Decompress_Text(actual_text)
            output.write(decompressed_text)
        print("The file is decompressed!!!")
        return   
try:
    path = input("ENTER THE PATH OF YOUR FILE....") 
    h = Huffmancode(path)
    compressed_file = h.compression()
    h.decompress(compressed_file)
except FileNotFoundError:
    print("No such file exists")
