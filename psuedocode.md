```bash
// Main Application Flow
FUNCTION runStudentCommuteOptimizer()
  // 1. Frontend: Get user's route input from the UI
  homeAddress = getInput('From:')
  schoolAddress = getInput('To:')

  // 2. Backend: Process the route and find matches
  //    - Geocode the addresses to get coordinates
  userRoute = geocode(homeAddress, schoolAddress)
  
  //    - Save the user's route in the system
  saveRoute(currentUser.id, userRoute)

  //    - Find other students with similar routes
  allRoutes = getAllActiveRoutes()
  potentialMatches = []

  FOREACH studentRoute IN allRoutes
    // Check for significant overlap between routes
    IF calculateOverlap(userRoute, studentRoute) > THRESHOLD
      potentialMatches.add(studentRoute.owner)
    END IF
  END FOREACH

  // 3. Frontend: Display the results
  displayMatchesOnMap(potentialMatches)

  // 4. Frontend: Handle user interaction
  onIconClick(selectedMatch)
    openChatWindow(currentUser, selectedMatch)
END FUNCTION
```
