-- ==============================================
-- KEYZORXZ HUB PRO
-- ==============================================

local OWNER_USERNAME = "keyler632"
local OWNER_USER_ID = 2043745142
local player = game.Players.LocalPlayer
local UIS = game:GetService("UserInputService")

local IS_OWNER = player.Name == OWNER_USERNAME or player.UserId == OWNER_USER_ID

if not IS_OWNER then
    player:Kick("No autorizado")
    return
end

-- FLAGS
local Flags = {
    AutoGlitch = false,
    AutoRebirth = false,
    AutoEquipment = false,
    AutoPets = false,
    AutoKing = false,
    AutoFarm = false,
    AutoDupePets = false
}

-- ==============================================
-- UI
-- ==============================================

local displayName = player.DisplayName or player.Name

local window = library:AddWindow("HYPER H | hi " .. displayName, {
    main_color = Color3.fromRGB(0, 0, 0),
    min_size = Vector2.new(400, 500),
    can_resize = false,
})

-- TABS
local FarmTab = window:AddTab("Farm")
local PetsTab = window:AddTab("Pets")
local KingTab = window:AddTab("King")
local MiscTab = window:AddTab("Misc")

FarmTab:Show()

-- ==============================================
-- FARM
-- ==============================================

FarmTab:AddSwitch("Auto Farm", function(state)
    Flags.AutoFarm = state
end)

FarmTab:AddSwitch("Auto Rebirth", function(state)
    Flags.AutoRebirth = state
end)

FarmTab:AddSwitch("Auto Glitch", function(state)
    Flags.AutoGlitch = state
end)

-- ==============================================
-- PETS
-- ==============================================

PetsTab:AddSwitch("Auto Pets", function(state)
    Flags.AutoPets = state
end)

PetsTab:AddSwitch("Auto Equipment", function(state)
    Flags.AutoEquipment = state
end)

PetsTab:AddSwitch("Auto Dupe Pets", function(state)
    Flags.AutoDupePets = state
end)

-- ==============================================
-- KING
-- ==============================================

KingTab:AddSwitch("Auto King", function(state)
    Flags.AutoKing = state
end)

-- ==============================================
-- MISC
-- ==============================================

MiscTab:AddButton("Print Stats", function()
    print(player.leaderstats)
end)

MiscTab:AddButton("Copy Username", function()
    setclipboard(player.Name)
end)

-- ==============================================
-- KEYBIND (MOSTRAR / OCULTAR)
-- ==============================================

local UIVisible = true

UIS.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end
    
    if input.KeyCode == Enum.KeyCode.RightControl then
        UIVisible = not UIVisible
        window:SetVisible(UIVisible)
    end
end)

-- ==============================================
-- SISTEMAS (LOOPS)
-- ==============================================

task.spawn(function()
    while true do
        if Flags.AutoGlitch then
            local r = game.ReplicatedStorage:FindFirstChild("GlitchPower", true)
            if r then r:FireServer(math.huge) end
        end
        task.wait(0.1)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoRebirth then
            local Power = player.leaderstats and player.leaderstats:FindFirstChild("Power", true)
            if Power and Power.Value >= 1e12 then
                print("Rebirth!")
            end
        end
        task.wait(0.5)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoFarm then
            print("Farming...")
        end
        task.wait(1)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoPets then
            print("Pets activos...")
        end
        task.wait(5)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoEquipment then
            print("Equipando...")
        end
        task.wait(5)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoKing then
            print("Modo King...")
        end
        task.wait(2)
    end
end)

task.spawn(function()
    while true do
        if Flags.AutoDupePets then
            print("Duplicando...")
        end
        task.wait(3)
    end
end)

-- ==============================================
-- NOTIFICACIÓN INICIAL
-- ==============================================

print("[HUB PRO] Cargado correctamente")
