DispatchGroup - 

    let dispatchGroup = DispatchGroup()
    dispatchGroup.enter()
    dispatchGroup.enter()
    someAsyncCall1
    {
         dispatchGroup.leave()
    }
    someAsyncCall2
    {
         dispatchGroup.leave()
    }
    dispatchGroup.notify(queue: .main) 
    {
         print("when call1 completes and calls2 completes this with execute")
    }

Example:


 @objc public func refreshData(completion: @escaping (Bool)->())
    {
        let dispatchGroup = DispatchGroup()
        var result:Bool = true
        
        dispatchGroup.enter()
        self.refreshUIProfile() 
        { (success:Bool, profile: Profile?, error:Error?) in
        
            dispatchGroup.leave()
        }
        
        dispatchGroup.enter()
        
        self.refreshMyAccount() 
        { (succes:Bool, error:Error?) in
          
            dispatchGroup.leave()
        }
        
        dispatchGroup.notify(queue: .main) 
        {
            completion(result)
        }
    }
