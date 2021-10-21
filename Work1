package main
import (
	"fmt"
)

func Read(readName chan string, exitChan chan bool) {
	for {
		v, ok := <- readName
		if !ok {
			break
		}
		fmt.Println("name = ", v)
	}

	exitChan<- true
	close(exitChan)
}

func Input(readName chan string, Name []string) {
	num := 0
	for i:= 0; i < 4; i++{
		readName<- Name[i]
		if i == 3 {
			i = -1
			num++
		}
		if num == 10{
			close(readName)
			break
		}
	}
}

func main() {
	readName := make(chan string, 40)
	exitChan := make(chan bool, 1)
	Name :=[4] string{"张三","李四","王五","赵六"} 

	go Input(readName,Name[:])
	go Read(readName, exitChan)

	for {
		_, ok := <-exitChan
		if !ok {
			break
		}
	}
}
