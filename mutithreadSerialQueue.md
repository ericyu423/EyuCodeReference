SerialQueue

      serialQueue = DispatchQueue(label: "MyQueue")
      serialQueue.async() 
            {
              self.myArray.removeAll()
            }

summmay: lock access (execute one at a time) using serialQueue

example:

      class AnalyticsHelper: NSObject
      {
          let myArray = Array()
          let serialQueue = DispatchQueue(label: "MyQueue")

          func remove()
          {
            serialQueue.async() 
            {
              self.myArray.removeAll()
            }
          }

          func add(event: myObjectType)
          {
            serialQueue.async() 
            {
              self.myArray.append(event)
            }
          }
      }

