-- Services
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")

-- Cache
local LocalPlayer = Players.LocalPlayer
local Mouse = LocalPlayer:GetMouse()
local CurrentCamera = workspace.CurrentCamera

-- Variables
local FindFirstChild = game.FindFirstChild
local Color3New = Color3.new
local Vector2New = Vector2.new
local DrawingNew = Drawing.new
local Round = math.round
local Tan = math.tan
local Random = math.random
local Rad = math.rad
local FindPartOnRayWithIgnoreList = workspace.FindPartOnRayWithIgnoreList
local CameraWorldToViewportPoint = CurrentCamera.WorldToViewportPoint
local UnbindFromRenderStep = RunService.UnbindFromRenderStep

-- Module
local Library = {
    Cache = {},
    Drawings = {},
    Options = {
        Enabled = false,
        VisibleOnly = false,
        Names = false,
        Boxes = false,
        BoxFill = false,
        Healthbars = false,
        HealthbarSize = 1,
        Distance = false,
        Tracers = false,
        WidthInStuds = 4,
        HeightInStuds = 5,
    },
    Colors = {
        Names = Color3New(1, 1, 1),
        Boxes = Color3New(1, 1, 1),
        BoxFill = Color3New(1, 1, 1),
        Healthbars = Color3New(0, 1, 0),
        Distance = Color3New(1, 1, 1),
        Tracers = Color3New(1, 1, 1),
    }
}

local function Create(Class, Properties)
    local Object = DrawingNew(Class)

    for Property, Value in pairs(Properties) do
        Object[Property] = Value
    end

    table.insert(Library.Drawings, Object)
    return Object
end

local function RoundVec(Vector)
    return Vector2New(Round(Vector.X), Round(Vector.Y))
end

local function WorldToViewportPoint(Position)
    local ScreenPos, OnScreen = CameraWorldToViewportPoint(CurrentCamera, Position)
    return Vector2New(ScreenPos.X, ScreenPos.Y), OnScreen, ScreenPos.Z
end

function Library.GetTeam(Player)
    return Player.Team
end

function Library.GetCharacter(Player)
    local Character = Player.Character
    return Character, Character and FindFirstChild(Character, "HumanoidRootPart")
end

function Library.VisibleCheck(Origin, Target, Character)
    local Part = FindPartOnRayWithIgnoreList(workspace, Ray.new(Origin, Target - Origin), { CurrentCamera, LocalPlayer.Character, Character }, false, true)
    return Part == nil
end

function Library.GetHealth(Character)
    local Humanoid = FindFirstChild(Character, "Humanoid")
    return Humanoid.Health, Humanoid.MaxHealth
end

function Library.AddEsp(Player)
    if (Player == LocalPlayer) then
        return
    end

    local Id = Random(-100000, 999999)

    local Objects = {
        Name = Create("Text", {
            Text = Player.Name,
            Size = 13,
            Center = true,
            Outline = true,
            OutlineColor = Color3New(),
            Font = 2,
            ZIndex = Id + 10
        }),
        Box = Create("Square", {
            Thickness = 1,
            ZIndex = Id + 9,
        }),
        BoxOutline = Create("Square", {
            Thickness = 3,
            Color = Color3New(),
            ZIndex = Id + 8
        }),
        BoxFill = Create("Square", {
            Thickness = 1,
            Transparency = 0.5,
            ZIndex = Id + 7,
            Filled = true,
        }),
        Healthbar = Create("Square", {
            Thickness = 1,
            Filled = true,
            ZIndex = Id + 6,
        }),
        HealthbarOutline = Create("Square", {
            Thickness = 3,
            Filled = true,
            Color = Color3New(),
            ZIndex = Id + 5
        }),
        Distance = Create("Text", {
            Size = 13,
            Center = true,
            Outline = true,
            OutlineColor = Color3New(),
            Font = 2,
            ZIndex = Id + 4
        }),
        Tracer = Create("Line", {
            Thickness = 1,
            ZIndex = Id + 3
        })
    }

    Library.Cache[Player] = Objects
end

function Library.RemoveEsp(Player)
    local Data = Library.Cache[Player]

    if (Data) then
        Library.Cache[Player] = nil

        for i,v in pairs(Data) do
            v:Remove()
        end
    end
end

function Library.Unload()
    UnbindFromRenderStep(RunService, "Esp Loop")

    for _, Player in pairs(Players:GetPlayers()) do
        Library.RemoveEsp(Player)
    end

    for _, Object in pairs(Library.Drawings) do
        Object:Destroy()
    end
end

function Library.Init()
    Players.PlayerAdded:Connect(function(Player)
        Library.AddEsp(Player)
    end)

    Players.PlayerRemoving:Connect(function(Player)
        Library.RemoveEsp(Player)
    end)

    RunService.BindToRenderStep(RunService, "Esp Loop", 1, function()
        for Player, Objects in pairs(Library.Cache) do
            if (Player ~= LocalPlayer and Library.GetTeam(Player) ~= Library.GetTeam(LocalPlayer)) then
                local Character, Torso = Library.GetCharacter(Player)

                if (Character and Torso) then
                    local TorsoPosition, OnScreen, Depth = WorldToViewportPoint(Torso.Position)

                    if (Library.Options.VisibleOnly and Library.VisibleCheck(CurrentCamera.CFrame.p, Torso.Position)) then
                        OnScreen = false
                    end

                    if (OnScreen and Library.Options.Enabled) then
                        local ScaleFactor = 1 / (Tan(Rad(CurrentCamera.FieldOfView / 2)) * 2 * Depth) * 1000
                        local Width, Height = Round(Library.Options.WidthInStuds * ScaleFactor), Round(Library.Options.HeightInStuds * ScaleFactor)
                        local X, Y = Round(TorsoPosition.X), Round(TorsoPosition.Y)
                        local BoxPosition = RoundVec(Vector2New(X - Width / 2, Y - Height / 2))
                        local BoxSize = Vector2New(Width, Height)
                        local Health, MaxHealth = Library.GetHealth(Character)
                        local HealthbarPosition = RoundVec(Vector2New(BoxPosition.X - (3 + Library.Options.HealthbarSize), BoxPosition.Y + BoxSize.Y))
                        local HealthbarSize = RoundVec(Vector2New(Library.Options.HealthbarSize, -BoxSize.Y))
                        local Magnitude = Round((CurrentCamera.CFrame.Position - Torso.Position).Magnitude)

                        Objects.Name.Visible = Library.Options.Names
                        Objects.Name.Color = Library.Colors.Names
                        Objects.Name.Position = Vector2New(X, BoxPosition.Y - 15)

                        Objects.Box.Visible = Library.Options.Boxes
                        Objects.Box.Color = Library.Colors.Boxes
                        Objects.Box.Position = BoxPosition
                        Objects.Box.Size = BoxSize

                        Objects.BoxOutline.Visible = Library.Options.Boxes
                        Objects.BoxOutline.Position = BoxPosition
                        Objects.BoxOutline.Size = BoxSize

                        Objects.BoxFill.Visible = Library.Options.BoxFill
                        Objects.BoxFill.Color = Library.Colors.BoxFill
                        Objects.BoxFill.Position = BoxPosition
                        Objects.BoxFill.Size = BoxSize

                        Objects.Healthbar.Visible = Library.Options.Healthbars
                        Objects.Healthbar.Color = Library.Colors.Healthbars
                        Objects.Healthbar.Position = HealthbarPosition
                        Objects.Healthbar.Size = RoundVec(Vector2New(HealthbarSize.X, HealthbarSize.Y * (Health / MaxHealth)))

                        Objects.HealthbarOutline.Visible = Library.Options.Healthbars
                        Objects.HealthbarOutline.Position = HealthbarPosition - Vector2New(1, -1)
                        Objects.HealthbarOutline.Size = HealthbarSize + Vector2New(2, -2)

                        Objects.Distance.Visible = Library.Options.Distance
                        Objects.Distance.Color = Library.Colors.Distance
                        Objects.Distance.Text = Magnitude .. " Studs"
                        Objects.Distance.Position = Vector2New(X, (BoxPosition.Y + BoxSize.Y) + 3)

                        Objects.Tracer.Visible = Library.Options.Tracers
                        Objects.Tracer.Color = Library.Colors.Tracers
                        Objects.Tracer.From = Vector2New(Mouse.X, Mouse.Y + 36)
                        Objects.Tracer.To = Vector2New(X, Y)
                    else
                        for i,v in pairs(Objects) do
                            v.Visible = false
                        end
                    end
                else
                    for i,v in pairs(Objects) do
                        v.Visible = false
                    end
                end
            else
                for i,v in pairs(Objects) do
                    v.Visible = false
                end
            end
        end
    end)

    for i,v in pairs(Players:GetPlayers()) do
        Library.AddEsp(v)
    end
end

return Library
