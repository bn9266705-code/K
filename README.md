local Player = game:GetService("Players").LocalPlayer
local insert = game:GetService("InsertService")
local Gradient = game:GetService("ReplicatedStorage").Assets.Meta.Gradients
local MainUI = Player.PlayerGui.MainUI
local Run = game["Run Service"]
local t = MainUI.InventoryScreen.InventoryRoot.SkinsContainer.Contents

local CurrentRig = Player.Character

local function TurnExclusive(Con)
  local G = Gradient.ExclusiveGradient:Clone()
  Con.Outline.ImageColor3 = Color3.new(1, 1, 1)
  G.Parent = Con.Outline
end

Run.Heartbeat:Connect(function()
  if t:FindFirstChild("Dued1Elliot") and t.Dued1Elliot:FindFirstChild("Container") and t.Dued1Elliot.Container:FindFirstChild("Outline") then
    if not t.Dued1Elliot.Container.Outline:FindFirstChild("ExclusiveGradient") then
      TurnExclusive(MainUI.InventoryScreen.InventoryRoot.SkinsContainer.Contents.Dued1Elliot.Container)
    end
  end
end)

local function import(link, name)
  if not isfile(name) then
    writefile(name, game:HttpGet(link))
  end
  return getcustomasset(name)
end

local ElliotLMS = import("https://github.com/bn9266705-code/007n7/raw/refs/heads/main/The_Remains_of_Robloxia_OST_-_FIGHT_BACK_(007n7_vs_Redacted).mp3.mpeg.mp3", "Elliot_LMS.mp3")

pcall(function()
  local Config = require(game:GetService("ReplicatedStorage").Assets.Skins.Survivors.Elliot.Dued1Elliot.Config)
  Config.RenderImage = "rbxassetid://104095141821276"
end)

local function CreatePart(name, parent, weld, offset)
  local Part = Instance.new("Part")
  Part.Name = name
  Part.Massless = true
  Part.Anchored = false
  Part.CanCollide = false
  Part.CanTouch = false
  Part.CanQuery = false
  if weld then
    local Weld = Instance.new("Weld")
    Weld.C0 = offset or CFrame.new(0, 0, 0)
    Weld.Part0 = Part
    Weld.Part1 = weld
    Weld.Parent = Part
  end
  Part.Parent = parent
  return Part
end

local function Accs(AccsName, parent, Mesh, Texture, Scale, CF, Welded, Angle)
  Scale = Scale or Vector3.new(1, 1, 1)
  Angle = Angle or CFrame.Angles(0, 0, 0)
  CF = CF or CFrame.new(0, 0, 0)
  local var_2 = CreatePart(AccsName, parent)
  var_2.Size = Vector3.new(1, 1, 1)
  local var_3 = Instance.new("SpecialMesh")
  var_3.Name = "Mesh"
  var_3.MeshId = Mesh
  var_3.TextureId = Texture
  var_3.Scale = Scale
  var_3.Parent = var_2
  local var_4 = Instance.new("Weld")
  var_4.C0 = CF * Angle
  var_4.Part0 = var_2
  var_4.Part1 = Welded
  var_4.Parent = var_2
  return var_2
end

local function Cloth(Id1, Id2, Id3, Parent)
  if Id1 ~= nil then
    local S = Instance.new("Shirt", Parent)
    S.ShirtTemplate = Id1
  end
  if Id2 ~= nil then
    local P = Instance.new("Pants", Parent)
    P.PantsTemplate = Id2
  end
  if Id3 ~= nil then
    local SG = Instance.new("ShirtGraphic", Parent)
    SG.Graphic = Id3
  end
end

local function D(...)
  for _, v in ipairs({...}) do
    if v then
      pcall(function() v:Destroy() end)
    end
  end
end

local function ClearAccessories(P)
  for _, v in ipairs(P:GetChildren()) do
    if v:IsA("Accessory") or v:IsA("Hat") or v:IsA("Shirt") or v:IsA("Pants") or v:IsA("ShirtGraphic") or v:IsA("CharacterMesh") then
      D(v)
    end
  end
  for _, v in ipairs(P:GetDescendants()) do
    if v:IsA("Accessory") or v:IsA("Hat") or v:IsA("Shirt") or v:IsA("Pants") or v:IsA("ShirtGraphic") or v:IsA("CharacterMesh") then
      D(v)
    end
  end
end

local C
local C2
local C3

local function clearC()
  if C then C:Disconnect() C = nil end
  if C2 then C2:Disconnect() C2 = nil end
  if C3 then C3:Disconnect() C3 = nil end
end

local function setupLMS(P)
  local Themes = workspace:FindFirstChild("Themes")
  if not Themes then
    task.spawn(function()
      Themes = workspace:WaitForChild("Themes", 60)
      if Themes then
        setupLMS(P)
      end
    end)
    return
  end
  C3 = Themes.ChildAdded:Connect(function(v)
    if not v:IsA("Sound") then return end
    task.wait(0.08)
    if v.Name == "LastSurvivor" or tostring(v.SoundId):find("80564889711353") then
      v.SoundId = ElliotLMS
      v.Volume = 1
      v:Play()
    end
  end)
end

local function DoMorph(P, Name, Skin)
  if P.Name == Name and P:GetAttribute("SkinName") == Skin then
    clearC()
    ClearAccessories(P)

    for _, v in ipairs({"Head", "Torso", "Left Arm", "Right Arm"}) do
      local L = P:WaitForChild(v)
      if L then
        L.Transparency = 0
        L.Color = Color3.fromRGB(175, 221, 255)
      end
    end

    for _, v in ipairs({"Left Leg", "Right Leg"}) do
      local L = P:WaitForChild(v)
      if L then
        L.Transparency = 0
        L.Color = Color3.fromRGB(27, 42, 53)
      end
    end

    Cloth("http://www.roblox.com/asset/?id=137090897548952", "http://www.roblox.com/asset/?id=133101841914139", nil, P)

    local Headphones = Accs("DJHeadphones", P, "rbxassetid://105190368943806", "rbxassetid://13296698898716", Vector3.new(1, 1, 1), CFrame.new(4.268e-29, 0.41, 0.015, -1, 0, 0, 0, 1, 0, 0, 0, -1), P.Head, nil)
    local HeadphonesWeld = Headphones:FindFirstChildOfClass("Weld")
    if HeadphonesWeld then
      HeadphonesWeld.C1 = CFrame.new(0, 0.6, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    end

    local Bandana = Accs("Dued1Bandana", P, "rbxassetid://131628909094953", "rbxassetid://101726942999936", Vector3.new(0.01, 0.01, 0.01), CFrame.new(0, 0.08, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1), P.Torso, nil)
    local BandanaWeld = Bandana:FindFirstChildOfClass("Weld")
    if BandanaWeld then
      BandanaWeld.C1 = CFrame.new(0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    end

    local Visor = Accs("Dued1WAAPVisor", P, "rbxassetid://93400563068446", "rbxassetid://117251502471573", Vector3.new(0.011, 0.011, 0.011), CFrame.new(0, 0.14, 0.33, 1, 0, 0, 0, 1, 0, 0, 0, 1), P.Head, nil)
    local VisorWeld = Visor:FindFirstChildOfClass("Weld")
    if VisorWeld then
      VisorWeld.C1 = CFrame.new(0, 0.6, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    end

    local Tailcoat = Accs("DarkBlueTailcoat", P, "rbxassetid://71589064423757", "rbxassetid://105930713797043", Vector3.new(1, 1, 1), CFrame.new(-3.815e-06, 0.65, 0.35, -1, 0, 0, 0, 1, 0, 0, 0, -1), P.Torso, nil)
    local TailcoatWeld = Tailcoat:FindFirstChildOfClass("Weld")
    if TailcoatWeld then
      TailcoatWeld.C1 = CFrame.new(0, -1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    end

    local Hair = Accs("UltraFabulousHair", P, "http://www.roblox.com/asset/?id=16627529", "http://www.roblox.com/asset/?id=16627494", Vector3.new(1.05, 1.05, 1.05), CFrame.new(8.658e-09, 0.1, -0.1, 1, 0, 0, 0, 1, 0, 0, 0, 1), P.Head, nil)
    local HairWeld = Hair:FindFirstChildOfClass("Weld")
    if HairWeld then
      HairWeld.C1 = CFrame.new(0, 0.6, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1)
    end

    setupLMS(P)

    C = P.Humanoid.Died:Once(clearC)
    C2 = Player.CharacterAdded:Once(clearC)
  end
end

DoMorph(CurrentRig, "Elliot", "Dued1Elliot")

Player.CharacterAdded:Connect(function(Rig)
  DoMorph(Rig, "Elliot", "Dued1Elliot")
end)
