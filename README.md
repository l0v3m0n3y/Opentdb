# Opentdb
api for opentdb.com site trivia questions generator
# main
```cpp
#include "Opentdb.h"
#include <iostream>

int main() {
   Opentdb api;

    auto trivias = api.random_trivias(10).then([](json::value result) {
        auto results = result.at("results").as_array();
        for (size_t i = 0; i < results.size(); ++i) {
            std::cout << results[i].at("category").as_string() << std::endl;
            std::cout << results[i].at("question").as_string() << std::endl;
           std::cout << results[i].at("correct_answer").as_string() << std::endl;
        }
    });
    trivias.wait();
    
    return 0;
}
```

# Launch (your script)
```
g++ -std=c++11 -o main main.cpp -lcpprest -lssl -lcrypto -lpthread -lboost_system -lboost_chrono -lboost_thread
./main
```

