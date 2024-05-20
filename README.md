#include <iostream>
#include <fstream>
#include <string>
#include <algorithm> // For std::reverse

// Function to append user input to the file
void appendToFile(const std::string& filename) {
    std::ofstream outFile(filename, std::ios::app); // Open file in append mode
    if (!outFile.is_open()) {
        std::cerr << "Error: Unable to open file for appending." << std::endl;
        return;
    }
    
    std::string userInput;
    std::cout << "Enter the data to append to the file: ";
    std::getline(std::cin, userInput);
    
    outFile << userInput << std::endl;
    outFile.close();
}

// Function to reverse the content of the file and store it in another file
void reverseFileContent(const std::string& inputFilename, const std::string& outputFilename) {
    std::ifstream inFile(inputFilename);
    if (!inFile.is_open()) {
        std::cerr << "Error: Unable to open input file for reading." << std::endl;
        return;
    }

    // Read entire file content into a string
    std::string fileContent((std::istreambuf_iterator<char>(inFile)), std::istreambuf_iterator<char>());
    inFile.close();

    // Reverse the file content
    std::reverse(fileContent.begin(), fileContent.end());

    // Write the reversed content to the output file
    std::ofstream outFile(outputFilename);
    if (!outFile.is_open()) {
        std::cerr << "Error: Unable to open output file for writing." << std::endl;
        return;
    }
    
    outFile << fileContent;
    outFile.close();
}

int main() {
    const std::string inputFilename = "CSC450_CT5_mod5.txt";
    const std::string outputFilename = "CSC450-mod5-reverse.txt";

    // Append user input to the file
    appendToFile(inputFilename);

    // Reverse the file content and store it in another file
    reverseFileContent(inputFilename, outputFilename);

    std::cout << "Operation completed successfully." << std::endl;

    return 0;
}
