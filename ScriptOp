local CONFIG = {
‎    DupeItemName = "BrainrotCrystal"
‎    DupeDelay = 0.05,
‎    AutoGrabRadius = 50,
‎    MoneyValueName = "leaderstats.Money",
‎    InfiniteJumpPower = 100,
‎}
‎
‎local function DupeItem(item)
‎    local replicatedStorage = game:GetService("ReplicatedStorage")
‎    local remoteDupe = replicatedStorage:FindFirstChild("ReplicateItem") or 
‎                       replicatedStorage:FindFirstChild("GiveItem") or
‎                       replicatedStorage:FindFirstChild("AddToInventory")
‎    if not remoteDupe then
‎        local player = game.Players.LocalPlayer
‎        local backpack = player:FindFirstChild("Backpack")
‎        if backpack then
‎            local newItem = item:Clone()
‎            newItem.Parent = backpack
‎            for i = 1, 10 do
‎                task.wait(CONFIG.DupeDelay)
‎                local copy = newItem:Clone()
‎                copy.Parent = backpack
‎            end
‎        end
‎        return
‎    end
‎    for i = 1, 100 do
‎        remoteDupe:FireServer(item)
‎        task.wait(CONFIG.DupeDelay)
‎    end
‎end
‎
‎local function AutoGrabBrainrot()
‎    local player = game.Players.LocalPlayer
‎    local character = player.Character or player.CharacterAdded:Wait()
‎    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
‎    
‎    game:GetService("RunService").RenderStepped:Connect(function()
‎        local brainrots = workspace:GetDescendants()
‎        for _, obj in ipairs(brainrots) do
‎            if obj:IsA("BasePart") and (string.find(obj.Name, "Brainrot") or string.find(obj.Name, "BrainRot")) then
‎                local distance = (obj.Position - humanoidRootPart.Position).Magnitude
‎                if distance <= CONFIG.AutoGrabRadius then
‎                    humanoidRootPart.CFrame = CFrame.new(obj.Position)
‎                    task.wait(0.1)
‎                    if obj:FindFirstChild("TouchInterest") then
‎                        firetouchinterest(humanoidRootPart, obj, 0)
‎                        firetouchinterest(humanoidRootPart, obj, 1)
‎                    end
‎                    local claimRemote = game:GetService("ReplicatedStorage"):FindFirstChild("ClaimBrainrot")
‎                    if claimRemote then
‎                        claimRemote:FireServer(obj)
‎                    end
‎                end
‎            end
‎        end
‎    end)
‎end
‎
‎local function InfiniteMoney()
‎    local player = game.Players.LocalPlayer
‎    local leaderstats = player:FindFirstChild("leaderstats")
‎    if not leaderstats then
‎        leaderstats = player:WaitForChild("leaderstats")
‎    end
‎    local money = leaderstats:FindFirstChild("Money") or leaderstats:FindFirstChild("Cash") or leaderstats:FindFirstChild("Coins")
‎    if money then
‎        if money.Changed then
‎            hookfunction(money.Changed, function(newValue)
‎                return
‎            end)
‎        end
‎        money.Value = 999999999
‎        game:GetService("RunService").Heartbeat:Connect(function()
‎            if money.Value < 999999999 then
‎                money.Value = 999999999
‎            end
‎        end)
‎    else
‎        local fakeMoney = Instance.new("IntValue")
‎        fakeMoney.Name = "FakeMoney"
‎        fakeMoney.Value = 999999999
‎        fakeMoney.Parent = player
‎    end
‎end
‎
‎local function InfiniteJump()
‎    local player = game.Players.LocalPlayer
‎    local character = player.Character or player.CharacterAdded:Wait()
‎    local humanoid = character:WaitForChild("Humanoid")
‎    humanoid.JumpPower = CONFIG.InfiniteJumpPower
‎    humanoid.UseJumpPower = true
‎    humanoid.Jump = true
‎    local UserInputService = game:GetService("UserInputService")
‎    UserInputService.JumpRequest:Connect(function()
‎        if humanoid and humanoid.FloorMaterial ~= Enum.Material.Air then
‎            humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
‎        elseif humanoid then
‎            humanoid:ChangeState(Enum.HumanoidStateType.Jumping)
‎        end
‎    end)
‎end
‎
‎local function OtherFeatures()
‎    local player = game.Players.LocalPlayer
‎    local character = player.Character or player.CharacterAdded:Wait()
‎    local humanoid = character:WaitForChild("Humanoid")
‎    humanoid.WalkSpeed = 100
‎    
‎    local noclipEnabled = true
‎    game:GetService("RunService").Stepped:Connect(function()
‎        if noclipEnabled and character and character.PrimaryPart then
‎            for _, part in ipairs(character:GetDescendants()) do
‎                if part:IsA("BasePart") then
‎                    part.CanCollide = false
‎                end
‎            end
‎        end
‎    end)
‎    
‎    local esp = Instance.new("Highlight")
‎    esp.Name = "BrainrotESP"
‎    esp.FillColor = Color3.fromRGB(255, 0, 255)
‎    esp.FillTransparency = 0.5
‎    esp.OutlineColor = Color3.fromRGB(0, 255, 0)
‎    esp.OutlineTransparency = 0
‎    game:GetService("RunService").RenderStepped:Connect(function()
‎        local brainrots = workspace:GetDescendants()
‎        for _, obj in ipairs(brainrots) do
‎            if obj:IsA("BasePart") and (string.find(obj.Name, "Brainrot") or string.find(obj.Name, "BrainRot")) then
‎                if not obj:FindFirstChild("BrainrotESP") then
‎                    local espClone = esp:Clone()
‎                    espClone.Parent = obj
‎                    espClone.Adornee = obj
‎                end
‎            end
‎        end
‎    end)
‎end
‎
‎print("[The Void Script] Loading...")
‎task.spawn(AutoGrabBrainrot)
‎task.spawn(InfiniteMoney)
‎task.spawn(InfiniteJump)
‎task.spawn(OtherFeatures)
‎
‎local function AutoDupeOnCollect()
‎    local player = game.Players.LocalPlayer
‎    local backpack = player:FindFirstChild("Backpack")
‎    if backpack then
‎        backpack.ChildAdded:Connect(function(child)
‎            if child:IsA("Tool") and string.find(child.Name, CONFIG.DupeItemName) then
‎                DupeItem(child)
‎            end
‎        end)
‎    end
‎end
‎task.spawn(AutoDupeOnCollect)
‎
‎print("[The Void Script] Active.")
‎
