
if value = -1 we wait
.wait() --value
.signal() ++value

example 0: ( this will not do anything)

1. init value = 0
2. .wait -> value = -1 (wait )

    let semaphore = DispatchSemaphore(value:0)
    let dispatchQueue = DispatchQueue.global(qos: .background)

    dispatchQueue.async {
        semaphore.wait()
        print("1")
        semaphore.signal()


        semaphore.wait()
        print("2")
        semaphore.signal()
    }
    print("0")

   output - 0

example 1:
  let semaphore = DispatchSemaphore(value:2)

  let dispatchQueue = DispatchQueue.global(qos: .background)
  dispatchQueue.async {
      semaphore.wait() // --value , if value = 0 go
      print("1")
      semaphore.wait()//-- value , if value = 0 go, if value is negative wait
      print("2")
      semaphore.wait()
      print("3")
  }
  print("0")

  output: 0, 1, 2
  
  
example 2:

    let semaphore = DispatchSemaphore(value:1)
    let dispatchQueue = DispatchQueue.global(qos: .background)

    dispatchQueue.async 
    {

        semaphore.wait()
        print("1")
        semaphore.signal()

        semaphore.wait()
        print("2")
        semaphore.signal()
    }
    print("0")

    print - 0, 1 , 2
