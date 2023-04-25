if game.PlaceId == 12860567360 then
    if not game:GetService("CoreGui"):FindFirstChild("nightmarefun") then
        game.Players.LocalPlayer.Character.Humanoid:UnequipTools()
        
        local Gui_Hub = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/nightmares.fun-UI-Library/main/source.lua"))()
        
        local Window = Gui_Hub.Create("Tao Hu")
        
        local Menu_1 = Window:Tab("Main")
        local Function_1 = Menu_1:Section("Auto Fram")
        
        local Function_2 = Menu_1:Section("Players")
        
        local Function_3 = Menu_1:Section("Teleport")
        
        local Function_4 = Menu_1:Section("Shop")
        
        local Menu_2 = Window:Tab("Setting / Credit")
        local Credit = Menu_2:Section("Gui")
        
        local Credit_2 = Menu_2:Section("Credit")
        
        
        Function_1:Label("Auto Fram Setting")
        
        
        EqTool = {}
        
        
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
            table.insert(EqTool, v.Name)
        end
        
        
        Function_1:Dropdown("Weapon Select", EqTool, function(Pick)
            _G.Tool = Pick
        end)
        
        
        Function_1:Dropdown("Mode Select", {"Under", "Behind", "Above"}, function(Pick)
            if Pick == "Under" then
                P_X = 0
                P_Y = -7
                P_Z = 0
                
                O_X = 600
                O_Y = 0
                O_Z = 0
            elseif Pick == "Behind" then
                P_X = 0
                P_Y = 0
                P_Z = 7
                
                O_X = 0
                O_Y = 0
                O_Z = 0
            elseif Pick == "Above" then
                P_X = 0
                P_Y =  7
                P_Z = 0
                
                O_X = 300
                O_Y = 0
                O_Z = 0
            end
        end)
        
        
        Function_1:Toggle("Instant Kill", function(s)
            if s then
                _G.Instant_Kill = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Instant_Kill then
                        pcall(function()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if _G.Instant_Kill and v.Humanoid.Health < v.Humanoid.MaxHealth/1.25 then
                                        v.Humanoid.Health = 0
                                        game:GetService("Workspace").FallenPartsDestroyHeight = 0 / 0
                                        sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", 1000)
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Instant_Kill = false
            end
        end)
        
        
        Function_1:Label("Auto Fram Levels")
        
        
        function CheckLvl()
            local Levels = game:GetService("Players").LocalPlayer.Data.Levels.Value
            if Levels == 1 or Levels <= 19 then
                Monster = "Blue People"
            elseif Levels == 20 or Levels <= 49 then
                Monster = "Tree Man"
            elseif Levels == 50 or Levels <= 99 then
                Monster = "Leaf Man"
            elseif Levels == 100 or Levels <= 301 then
                Monster = "Snow People"
            elseif Levels == 302 or Levels <= 401 then
                Monster = "Sky Bandit"
            elseif Levels == 402 or Levels <= 601 then
                Monster = "Sky Js"
            elseif Levels == 602 or Levels <= 650 then
                Monster = "Hole"
            elseif Levels == 651 or Levels <= 701 then
                Monster = "Lok Lek"
            elseif Levels == 702 or Levels <= 801 then
                Monster = "Treeหลังอย่าคิดไปใกล"
            elseif Levels == 802 or Levels <= 850 then
                Monster = "Sand Bandit"
            elseif Levels == 851 or Levels <= 901 then
                Monster = "Sang"
            elseif Levels == 902 or Levels <= 1001 then
                Monster = "Sand Man"
            end
        end
        
        
        Function_1:Toggle("Auto Fram Levels", function(s)
            if s then
                _G.Auto_Fram = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Auto_Fram then
                        pcall(function()
                            CheckLvl()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if v.Name == Monster and v.Humanoid.Health > 0 then
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(P_X, P_Y, P_Z) * CFrame.fromOrientation(O_X, O_Y, O_Z)
                                        setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                        game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
                                        
                                        
                                        if not game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) and _G.Auto_Fram == true then
                                            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack[_G.Tool])
                                        elseif game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) then
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1166, 898))  
                                        end
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Auto_Fram = false
            end
        end)
        
        
        Function_1:Button("Fix Instant Kill", function()
            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                for i,v in pairs(v:GetChildren()) do
                    if v.Humanoid.Health == 0 then
                        v.Humanoid.Health = v.Humanoid.MaxHealth
                    end
                end
            end
        end)
        
        
        Function_1:Label("Auto Fram Select")
        
        
        Function_1:Dropdown("Auto Fram Select", {"Bad People","Blue People","Tree Man","Leaf Man","Snow People","People love Plar UwU","Tree Boss","Leaf Boss","YeTood","Leaf Noob","Sand Stone","Sand boss"}, function(Pick)
            _G.Monster = Pick
        end)
        
        
        Function_1:Toggle("Auto Fram Select", function(s)
            if s then
                _G.Auto_Fram_Select = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Auto_Fram_Select then
                        pcall(function()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if v.Name == _G.Monster and v.Humanoid.Health > 0 then
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(P_X, P_Y, P_Z) * CFrame.fromOrientation(O_X, O_Y, O_Z)
                                        setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                        game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
                                        if not game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) then
                                            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack[_G.Tool])
                                        else
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1166, 898))  
                                        end
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Auto_Fram_Select = false
            end
        end)
        
        
        Function_1:Button("Fix Instant Kill", function()
            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                for i,v in pairs(v:GetChildren()) do
                    if v.Humanoid.Health == 0 then
                        v.Humanoid.Health = v.Humanoid.MaxHealth
                    end
                end
            end
        end)
        
        
        Function_2:Label("Players")
        
        
        PlrS = {}
        
        
        for i,v in pairs(game.Players:GetChildren()) do
            if v.Name ~= game.Players.LocalPlayer.Name then
                table.insert(PlrS, v.Name)
            end
        end
        
        
        Function_2:Dropdown("Player Select", PlrS, function(Pick)
            _G.PlrPick = Pick
        end)
        
        
        Function_2:Button("Teleport To Player", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[_G.PlrPick].Character.HumanoidRootPart.CFrame
        end)
        
        
        Function_2:Toggle("View This Player", function(s)
            if s then
                game:GetService("Workspace").Camera.CameraSubject = game.Players[_G.PlrPick].Character.Humanoid
            else
               game:GetService("Workspace").Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
            end
        end)
        
        
        Function_2:Toggle("Bring This Player", function(s)
            if s then
                _G.Kill = true
                
                
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Kill then
                        pcall(function()
                            game.Players[_G.PlrPick].Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -4)
                            setfflag("HumanoidParallelRemoveNoPhysics", "False")
                            setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                            game:GetService("Players")[_G.PlrPick].Character.Humanoid:ChangeState(11)
                        end)
                    end
                end)
            else
               _G.Kill = false
            end
        end)
        
        
        Function_2:Toggle("Bring All", function(s)
            if s then
                _G.KillAll = true
                
                
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.KillAll then
                        pcall(function()
                            for i,v in pairs(game.Players:GetChildren()) do
                                if v.Name ~= game.Players.LocalPlayer.Name and v.Players_Setting.PvP.Value == true then
                                    v.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -4)
                                    setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                    v.Character.Humanoid:ChangeState(11)
                                end
                            end
                        end)
                    end
                end)
            else
               _G.KillAll = false
            end
        end)
        
        
        Function_3:Button("Starter Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-17.8772469, 10.4073277, -682.160034, -0.999869347, 6.07082296e-09, -0.0161655191, 6.02664141e-09, 1, 2.78179213e-09, 0.0161655191, 2.6840048e-09, -0.999869347)
        end)
        
        
        Function_3:Button("Jungle Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(672.556641, 7.18790483, 625.724304, 0.0156977009, 4.08574596e-09, -0.999876797, 1.18003562e-08, 1, 4.2715107e-09, 0.999876797, -1.18659553e-08, 0.0156977009)
        end)
        
        
        Function_3:Button("Waterfall Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(140.660721, 9943.08203, -2.49934506, -0.0272740014, 1.05700844e-08, 0.999628007, 2.9460312e-09, 1, -1.0493638e-08, -0.999628007, 2.6587319e-09, -0.0272740014)
        end)
        
        
        Function_3:Button("Snow Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-797.238281, 9.71098328, 235.62413, 0.00243704999, -9.70730483e-08, 0.99999702, -7.09934866e-08, 1, 9.72463496e-08, -0.99999702, -7.12302679e-08, 0.00243704999)
        end)
        
        
        Function_3:Button("Boss Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1012.09857, 23.2328873, -439.883392, 0.187807962, 5.02110398e-09, -0.982205749, -5.54697976e-08, 1, -5.49433388e-09, 0.982205749, 5.55146364e-08, 0.187807962)
        end)
        
        
        Function_4:Button("Mini Gun Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Mini Gun Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Mini Gun Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Cut Sword Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Cut Sword Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Cut Sword Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Big Gun Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Big Gun Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Big Gun Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Random Glue", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Random Glue"].CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Random Glue"].ProximityPrompt)
        end)
        
        
        Credit:Label("Close / Open Gui")
        
        
        Credit:KeyBind("KeyBind", Enum.KeyCode.RightControl, function()
            if game:GetService("CoreGui").nightmarefun.Enabled == true then
                game:GetService("CoreGui").nightmarefun.Enabled = false
            else
                game:GetService("CoreGui").nightmarefun.Enabled = true
            end
        end)
        
        
        Credit_2:Button("Discord Offical", function()
            setclipboard("https://discord.gg/6MP3MRbDW5")
        end)
    else
        game:GetService("CoreGui").nightmarefun:Destroy()
        
        game.Players.LocalPlayer.Character.Humanoid:UnequipTools()
        
        local Gui_Hub = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/nightmares.fun-UI-Library/main/source.lua"))()
        
        local Window = Gui_Hub.Create("Tao Hu")
        
        local Menu_1 = Window:Tab("Main")
        local Function_1 = Menu_1:Section("Auto Fram")
        
        local Function_2 = Menu_1:Section("Players")
        
        local Function_3 = Menu_1:Section("Teleport")
        
        local Function_4 = Menu_1:Section("Shop")
        
        local Menu_2 = Window:Tab("Setting / Credit")
        local Credit = Menu_2:Section("Gui")
        
        local Credit_2 = Menu_2:Section("Credit")
        
        
        Function_1:Label("Auto Fram Setting")
        
        
        EqTool = {}
        
        
        for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
            table.insert(EqTool, v.Name)
        end
        
        
        Function_1:Dropdown("Weapon Select", EqTool, function(Pick)
            _G.Tool = Pick
        end)
        
        
        Function_1:Dropdown("Mode Select", {"Under", "Behind", "Above"}, function(Pick)
            if Pick == "Under" then
                P_X = 0
                P_Y = -7
                P_Z = 0
                
                O_X = 600
                O_Y = 0
                O_Z = 0
            elseif Pick == "Behind" then
                P_X = 0
                P_Y = 0
                P_Z = 7
                
                O_X = 0
                O_Y = 0
                O_Z = 0
            elseif Pick == "Above" then
                P_X = 0
                P_Y =  7
                P_Z = 0
                
                O_X = 300
                O_Y = 0
                O_Z = 0
            end
        end)
        
        
        Function_1:Toggle("Instant Kill", function(s)
            if s then
                _G.Instant_Kill = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Instant_Kill then
                        pcall(function()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if _G.Instant_Kill and v.Humanoid.Health < v.Humanoid.MaxHealth/1.25 then
                                        v.Humanoid.Health = 0
                                        game:GetService("Workspace").FallenPartsDestroyHeight = 0 / 0
                                        sethiddenproperty(game:GetService("Players").LocalPlayer, "SimulationRadius", 1000)
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Instant_Kill = false
            end
        end)
        
        
        Function_1:Label("Auto Fram Levels")
        
        
        function CheckLvl()
            local Levels = game:GetService("Players").LocalPlayer.Data.Levels.Value
            if Levels == 1 or Levels <= 19 then
                Monster = "Blue People"
            elseif Levels == 20 or Levels <= 49 then
                Monster = "Tree Man"
            elseif Levels == 50 or Levels <= 99 then
                Monster = "Leaf Man"
            elseif Levels == 100 or Levels <= 301 then
                Monster = "Snow People"
            elseif Levels == 302 or Levels <= 401 then
                Monster = "Sky Bandit"
            elseif Levels == 402 or Levels <= 601 then
                Monster = "Sky Js"
            elseif Levels == 602 or Levels <= 650 then
                Monster = "Hole"
            elseif Levels == 651 or Levels <= 701 then
                Monster = "Lok Lek"
            elseif Levels == 702 or Levels <= 801 then
                Monster = "Treeหลังอย่าคิดไปใกล"
            elseif Levels == 802 or Levels <= 850 then
                Monster = "Sand Bandit"
            elseif Levels == 851 or Levels <= 901 then
                Monster = "Sang"
            elseif Levels == 902 or Levels <= 1001 then
                Monster = "Sand Man"
            end
        end
        
        
        Function_1:Toggle("Auto Fram Levels", function(s)
            if s then
                _G.Auto_Fram = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Auto_Fram then
                        pcall(function()
                            CheckLvl()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if v.Name == Monster and v.Humanoid.Health > 0 then
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(P_X, P_Y, P_Z) * CFrame.fromOrientation(O_X, O_Y, O_Z)
                                        setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                        game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
                                        
                                        
                                        if not game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) and _G.Auto_Fram == true then
                                            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack[_G.Tool])
                                        elseif game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) then
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1166, 898))  
                                        end
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Auto_Fram = false
            end
        end)
        
        
        Function_1:Button("Fix Instant Kill", function()
            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                for i,v in pairs(v:GetChildren()) do
                    if v.Humanoid.Health == 0 then
                        v.Humanoid.Health = v.Humanoid.MaxHealth
                    end
                end
            end
        end)
        
        
        Function_1:Label("Auto Fram Select")
        
        
        Function_1:Dropdown("Auto Fram Select", {"Bad People","Blue People","Tree Man","Leaf Man","Snow People","People love Plar UwU","Tree Boss","Leaf Boss","YeTood","Leaf Noob","Sand Stone "," Sand boss"}, function(Pick)
            _G.Monster = Pick
        end)
        
        
        Function_1:Toggle("Auto Fram Select", function(s)
            if s then
                _G.Auto_Fram_Select = true
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Auto_Fram_Select then
                        pcall(function()
                            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                                for i,v in pairs(v:GetChildren()) do
                                    if v.Name == _G.Monster and v.Humanoid.Health > 0 then
                                        v.Humanoid.JumpPower = 0
                                        v.Humanoid.WalkSpeed = 0
                                        
                                        game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = v.HumanoidRootPart.CFrame * CFrame.new(P_X, P_Y, P_Z) * CFrame.fromOrientation(O_X, O_Y, O_Z)
                                        setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                        game:GetService("Players").LocalPlayer.Character.Humanoid:ChangeState(11)
                                        if not game.Players.LocalPlayer.Character:FindFirstChild(_G.Tool) then
                                            game.Players.LocalPlayer.Character.Humanoid:EquipTool(game.Players.LocalPlayer.Backpack[_G.Tool])
                                        else
                                            game:GetService("VirtualUser"):CaptureController()
                                            game:GetService("VirtualUser"):Button1Down(Vector2.new(1166, 898))  
                                        end
                                    end
                                end
                            end
                        end)
                    end
                end)
            else
                _G.Auto_Fram_Select = false
            end
        end)
        
        
        Function_1:Button("Fix Instant Kill", function()
            for i,v in pairs(game:GetService("Workspace").Monster:GetChildren()) do
                for i,v in pairs(v:GetChildren()) do
                    if v.Humanoid.Health == 0 then
                        v.Humanoid.Health = v.Humanoid.MaxHealth
                    end
                end
            end
        end)
        
        
        Function_2:Label("Players")
        
        
        PlrS = {}
        
        
        for i,v in pairs(game.Players:GetChildren()) do
            if v.Name ~= game.Players.LocalPlayer.Name then
                table.insert(PlrS, v.Name)
            end
        end
        
        
        Function_2:Dropdown("Player Select", PlrS, function(Pick)
            _G.PlrPick = Pick
        end)
        
        
        Function_2:Button("Teleport To Player", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[_G.PlrPick].Character.HumanoidRootPart.CFrame
        end)
        
        
        Function_2:Toggle("View This Player", function(s)
            if s then
                game:GetService("Workspace").Camera.CameraSubject = game.Players[_G.PlrPick].Character.Humanoid
            else
               game:GetService("Workspace").Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
            end
        end)
        
        
        Function_2:Toggle("Bring This Player", function(s)
            if s then
                _G.Kill = true
                
                
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.Kill then
                        pcall(function()
                            game.Players[_G.PlrPick].Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -4)
                            setfflag("HumanoidParallelRemoveNoPhysics", "False")
                            setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                            game:GetService("Players")[_G.PlrPick].Character.Humanoid:ChangeState(11)
                        end)
                    end
                end)
            else
               _G.Kill = false
            end
        end)
        
        
        Function_2:Toggle("Bring All", function(s)
            if s then
                _G.KillAll = true
                
                
                game:GetService("RunService").RenderStepped:Connect(function()
                    if _G.KillAll then
                        pcall(function()
                            for i,v in pairs(game.Players:GetChildren()) do
                                if v.Name ~= game.Players.LocalPlayer.Name and v.Players_Setting.PvP.Value == true then
                                    v.Character.HumanoidRootPart.CFrame = game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame * CFrame.new(0, 0, -4)
                                    setfflag("HumanoidParallelRemoveNoPhysics", "False")
                                    setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
                                    v.Character.Humanoid:ChangeState(11)
                                end
                            end
                        end)
                    end
                end)
            else
               _G.KillAll = false
            end
        end)
        
        
        Function_3:Button("Starter Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-17.8772469, 10.4073277, -682.160034, -0.999869347, 6.07082296e-09, -0.0161655191, 6.02664141e-09, 1, 2.78179213e-09, 0.0161655191, 2.6840048e-09, -0.999869347)
        end)
        
        
        Function_3:Button("Jungle Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(672.556641, 7.18790483, 625.724304, 0.0156977009, 4.08574596e-09, -0.999876797, 1.18003562e-08, 1, 4.2715107e-09, 0.999876797, -1.18659553e-08, 0.0156977009)
        end)
        
        
        Function_3:Button("Waterfall Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(140.660721, 9943.08203, -2.49934506, -0.0272740014, 1.05700844e-08, 0.999628007, 2.9460312e-09, 1, -1.0493638e-08, -0.999628007, 2.6587319e-09, -0.0272740014)
        end)
        
        
        Function_3:Button("Snow Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-797.238281, 9.71098328, 235.62413, 0.00243704999, -9.70730483e-08, 0.99999702, -7.09934866e-08, 1, 9.72463496e-08, -0.99999702, -7.12302679e-08, 0.00243704999)
        end)
        
        
        Function_3:Button("Boss Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1012.09857, 23.2328873, -439.883392, 0.187807962, 5.02110398e-09, -0.982205749, -5.54697976e-08, 1, -5.49433388e-09, 0.982205749, 5.55146364e-08, 0.187807962)
        end)
        
        
        Function_3:Button("Songkran Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(-286.932312, 9.71764469, 364.651154, -0.998904943, -4.87499019e-09, 0.0467857383, -2.50359999e-09, 1, 5.07447702e-08, -0.0467857383, 5.05720692e-08, -0.998904943)
        end) 
        
        
        Function_3:Button("Sand Island", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(1088.64526, 17.8685951, 1685.20276, 0.0112204188, -2.54215848e-09, 0.999937057, -2.62054689e-09, 1, 2.57172417e-09, -0.999937057, -2.64923772e-09, 0.0112204188)
        end) 
        
        
        Function_4:Button("Mini Gun Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Mini Gun Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Mini Gun Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Cut Sword Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Cut Sword Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Cut Sword Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Big Gun Shop", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Big Gun Shop"].EPart.CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Big Gun Shop"].EPart.ProximityPrompt)
        end)
        
        
        Function_4:Button("Random Glue", function()
            game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game:GetService("Workspace").Shop["Random Glue"].CFrame
            fireproximityprompt(game:GetService("Workspace").Shop["Random Glue"].ProximityPrompt)
        end)
        
        
        Credit:Label("Close / Open Gui")
        
        
        Credit:KeyBind("KeyBind", Enum.KeyCode.RightControl, function()
            if game:GetService("CoreGui").nightmarefun.Enabled == true then
                game:GetService("CoreGui").nightmarefun.Enabled = false
            else
                game:GetService("CoreGui").nightmarefun.Enabled = true
            end
        end)
        
        
        Credit_2:Button("Discord Offical", function()
            setclipboard("https://discord.gg/6MP3MRbDW5")
        end)
    end
end
