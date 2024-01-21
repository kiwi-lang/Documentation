Initialization

0. AGKFogOfWarVolume::PreInitializeComponents
   -> Cleanup States
   -> Prepare Material Parameter Collection

1. GameMode::StartPlay
   -> AGKFogOfWarVolume::InitializeServer
      - Instantiate a AGKFogOfWarTeam for each teams
      - Initialize Strategy
      - Server is Ready

   ->

