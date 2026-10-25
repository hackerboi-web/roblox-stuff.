local Rayfield = loadstring(game:HttpGet('https://sirius.menu/gen2'))()

if _G.BFP and _G.BFP.stop then pcall(_G.BFP.stop) end

local Players      = game:GetService("Players")
local RS           = game:GetService("ReplicatedStorage")
local RunService   = game:GetService("RunService")
local TweenService = game:GetService("TweenService")
local PathService  = game:GetService("PathfindingService")
local VirtualUser  = game:GetService("VirtualUser")
local VIM          = game:GetService("VirtualInputManager")
local player       = Players.LocalPlayer

local CFG = {
    Target             = nil,
    MaxWalk            = 1200,
    Weapon             = nil,
    AutoBuso           = true,
    AutoKen            = true,
    KenEvery           = 300,
    M1                 = true,
    SkillZ             = false,
    SkillX             = false,
    SkillC             = false,
    SkillV             = false,
    SkillEvery         = 4,
    SwingMin           = 0.12,
    SwingMax           = 0.30,
    FastAttack         = false,
    AttackSpeed        = 0.35,
    Dash               = false,
    DashFrom           = 25,
    DashCooldown       = 0.9,
    DashKey            = "Q",
    DashTurnsCamera    = true,
    StandOff           = 8,
    StandSlack         = 2,
    SwingFrom          = 30,
    FaceLock           = true,
    AimCamera          = false,
    CamBack            = 13,
    CamUp              = 5,
    QuestLoop          = true,
    GiverMode          = "auto",
    GiverWalkRadius    = 250,
    QuestReturnToFarm  = true,
    QuestGiverName     = nil,
    QuestName          = nil,
    QuestTier          = nil,
    QuestGiverRange    = 1200,
    QuestRetrySeconds  = 8,
    QuestStallSeconds  = 240,
    QuestKillsFallback = 10,
    MinHealthPercent   = 0.30,
    RegenWait          = 6,
    RestMin            = 0,
    RestMax            = 0,
    SweepSeconds       = 10,
    StuckSeconds       = 30,
    GiveUpSeconds      = 12,
    Gather             = true,
    GatherCount        = 3,
    GatherRadius       = 60,
    GatherCooldown     = 6,
    JumpWhenStuck      = true,
    Panic              = true,
    ClimbJumps         = 8,
    TerrainMap         = true,
    Ghost              = true,
    GhostAfter         = 1.5,
    GhostLiftMax       = 30,
    Debug              = false,
}

local P = { running = false, config = CFG }
_G.BFP = P

local LEVELS = {
    {1,9,"Bandit",Vector3.new(1059.4,16.5,1546.6)},
    {10,14,"Monkey",Vector3.new(-1445.1,23.5,-48.8)},
    {15,29,"Gorilla",Vector3.new(-1119.8,40.5,1839.0)},
    {30,39,"Pirate",Vector3.new(-1181.3,4.5,3803.5)},
    {40,59,"Brute",Vector3.new(-1145.2,14.8,4321.7)},
    {60,74,"Desert Bandit",Vector3.new(932.2,6.5,4482.0)},
    {75,89,"Desert Officer",Vector3.new(1609.1,6.5,4369.8)},
    {90,99,"Snow Bandit",Vector3.new(1386.8,87.3,-1297.1)},
    {100,119,"Snowman",Vector3.new(1198.2,105.5,-1237.0)},
    {120,149,"Chief Petty Officer",Vector3.new(-4881.1,4.5,4257.4)},
    {150,174,"Sky Bandit",Vector3.new(-4841.7,717.8,-2666.9)},
    {175,189,"Dark Master",Vector3.new(-5217.1,12.5,-4836.7)},
    {190,209,"Prisoner",Vector3.new(5309.8,0.5,475.5)},
    {210,249,"Dangerous Prisoner",Vector3.new(5086.1,2,466.4)},
    {250,274,"Toga Warrior",Vector3.new(-3625.0,7.5,-3003.7)},
    {275,299,"Gladiator",Vector3.new(-1309.9,7.5,-3251.6)},
    {300,324,"Military Soldier",Vector3.new(-5316.2,12.5,-2842.5)},
    {325,374,"Military Spy",Vector3.new(-5815.4,84.5,-8972.3)},
    {375,399,"Fishman Warrior",Vector3.new(61122.7,18.5,1569.1)},
    {400,449,"Fishman Commando",Vector3.new(61922.6,18.5,1493.9)},
    {450,474,"God's Guard",Vector3.new(-4721.9,845.3,-1954.4)},
    {475,524,"Shanda",Vector3.new(-7685.1,5567.8,-502.1)},
    {525,549,"Royal Squad",Vector3.new(-7665.2,5839.5,-1818.8)},
    {550,624,"Royal Soldier",Vector3.new(-7836.8,5607.8,-1540.5)},
    {625,649,"Galley Pirate",Vector3.new(5551.0,42.5,3946.3)},
    {650,699,"Galley Captain",Vector3.new(5436.0,38.5,4757.8)},
    {700,724,"Raider",Vector3.new(68.9,93.6,2429.7)},
    {725,774,"Mercenary",Vector3.new(-864.9,122.5,1453.2)},
    {775,799,"Swan Pirate",Vector3.new(1065.4,137.6,1324.4)},
    {800,874,"Factory Staff",Vector3.new(533.2,128.5,355.6)},
    {875,899,"Marine Lieutenant",Vector3.new(-2489.3,84.6,-3151.9)},
    {900,949,"Marine Captain",Vector3.new(-2335.2,79.8,-3245.9)},
    {950,974,"Zombie",Vector3.new(-5536.5,101.1,-835.6)},
    {975,999,"Vampire",Vector3.new(-5806.1,16.7,-1164.4)},
    {1000,1049,"Snow Trooper",Vector3.new(535.2,432.7,-5484.9)},
    {1050,1099,"Winter Warrior",Vector3.new(1234.5,457.0,-5174.1)},
    {1100,1124,"Lab Subordinate",Vector3.new(-5720.6,63.3,-4784.6)},
    {1125,1174,"Horned Warrior",Vector3.new(-6292.8,91.2,-5502.7)},
    {1175,1199,"Magma Ninja",Vector3.new(-5461.8,130.4,-5836.5)},
    {1200,1249,"Lava Pirate",Vector3.new(-5251.2,55.2,-4774.4)},
    {1250,1274,"Ship Deckhand",Vector3.new(921.1,126.0,33088.3)},
    {1275,1299,"Ship Engineer",Vector3.new(886.3,40.5,32800.8)},
    {1300,1324,"Ship Steward",Vector3.new(943.9,129.6,33444.4)},
    {1325,1349,"Ship Officer",Vector3.new(955.4,181.1,33331.9)},
    {1350,1374,"Arctic Warrior",Vector3.new(5935.5,77.3,-6472.8)},
    {1375,1424,"Snow Lurker",Vector3.new(5628.5,57.6,-6618.4)},
    {1425,1449,"Sea Soldier",Vector3.new(-3185.0,58.8,-9663.6)},
    {1450,1499,"Water Fighter",Vector3.new(-3262.9,298.7,-10552.5)},
    {1500,1524,"Pirate Millionaire",Vector3.new(81.2,43.8,5724.7)},
    {1525,1574,"Pistol Billionaire",Vector3.new(81.2,43.8,5724.7)},
    {1575,1599,"Dragon Crew Warrior",Vector3.new(6242.0,51.5,-1244.0)},
    {1600,1624,"Dragon Crew Archer",Vector3.new(6488.9,383.4,-110.7)},
    {1625,1649,"Female Islander",Vector3.new(5825.2,682.9,704.6)},
    {1650,1699,"Giant Islander",Vector3.new(4530.4,656.8,-131.6)},
    {1700,1724,"Marine Commodore",Vector3.new(2490.1,190.4,-7160.1)},
    {1725,1774,"Marine Rear Admiral",Vector3.new(3951.4,229.1,-6912.8)},
    {1775,1799,"Fishman Raider",Vector3.new(-10322.4,390.9,-8580.1)},
    {1800,1824,"Fishman Captain",Vector3.new(-11194.5,442.0,-8608.8)},
    {1825,1849,"Forest Pirate",Vector3.new(-13225.8,428.2,-7753.1)},
    {1850,1899,"Mythological Pirate",Vector3.new(-13869.2,565.0,-7084.4)},
    {1900,1924,"Jungle Pirate",Vector3.new(-11982.2,376.3,-10451.4)},
    {1925,1974,"Musketeer Pirate",Vector3.new(-13282.3,496.2,-9565.2)},
    {1975,1999,"Reborn Skeleton",Vector3.new(-8817.9,191.2,6298.7)},
    {2000,2024,"Living Zombie",Vector3.new(-10125.2,184.0,6242.0)},
    {2025,2049,"Demonic Soul",Vector3.new(-9712.0,204.7,6193.3)},
    {2050,2074,"Posessed Mummy",Vector3.new(-9545.8,69.6,6339.6)},
    {2075,2099,"Peanut Scout",Vector3.new(-2126.4,90.6,-10302.0)},
    {2100,2124,"Peanut President",Vector3.new(-2118.8,70.3,-10509.3)},
    {2125,2149,"Ice Cream Chef",Vector3.new(-685.3,96.3,-10957.6)},
    {2150,2199,"Ice Cream Commander",Vector3.new(-635.7,143.0,-11335.2)},
    {2200,2224,"Cookie Crafter",Vector3.new(-2321.7,36.7,-12216.7)},
    {2225,2249,"Cake Guard",Vector3.new(-1418.1,36.7,-12255.7)},
    {2250,2274,"Baking Staff",Vector3.new(-1980.4,36.7,-12983.8)},
    {2275,2299,"Head Baker",Vector3.new(-2251.6,52.3,-13033.4)},
    {2300,2324,"Cocoa Warrior",Vector3.new(168.0,26.2,-12238.9)},
    {2325,2349,"Chocolate Bar Battler",Vector3.new(701.3,25.6,-12708.2)},
    {2350,2374,"Sweet Thief",Vector3.new(-140.3,25.6,-12652.3)},
    {2375,2399,"Candy Rebel",Vector3.new(47.9,25.6,-13029.2)},
    {2400,2424,"Candy Pirate",Vector3.new(-1437.6,17.1,-14385.7)},
    {2425,2449,"Snow Demon",Vector3.new(-916.2,17.1,-14638.8)},
    {2450,2474,"Isle Outlaw",Vector3.new(-16162.8,11.7,-96.5)},
    {2475,2499,"Island Boy",Vector3.new(-16357.3,20.6,1005.6)},
    {2500,2524,"Sun-kissed Warrior",Vector3.new(-16357.3,20.6,1005.6)},
    {2525,2549,"Isle Champion",Vector3.new(-16848.9,21.7,1041.4)},
    {2550,2574,"Serpent Hunter",Vector3.new(-16621.4,121.4,1290.7)},
    {2575,2600,"Skull Slayer",Vector3.new(-16811.6,84.6,1542.2)},
    {2600,2624,"Reef Bandit",Vector3.new(10943.1,-2083.0,9177.3)},
    {2625,2649,"Coral Pirate",Vector3.new(10713.4,-2093.0,9307.1)},
    {2650,2674,"Sea Chanter",Vector3.new(10647.6,-2077.6,10080.0)},
    {2675,2699,"Ocean Prophet",Vector3.new(11056.1,-2001.7,10117.4)},
    {2700,2724,"High Disciple",Vector3.new(9843.6,-1993.5,9696.5)},
    {2725,2800,"Grand Devotee",Vector3.new(9591.1,-1993.5,9808.7)},
}
P.levels = LEVELS

local QUESTS = {
    ["Bandit"]                = { "BanditQuest1", 1 },
    ["Monkey"]                = { "JungleQuest", 1 },
    ["Gorilla"]               = { "JungleQuest", 2 },
    ["Pirate"]                = { "BuggyQuest1", 1 },
    ["Brute"]                 = { "BuggyQuest1", 2 },
    ["Desert Bandit"]         = { "DesertQuest", 1 },
    ["Desert Officer"]        = { "DesertQuest", 2 },
    ["Snow Bandit"]           = { "SnowQuest", 1 },
    ["Snowman"]               = { "SnowQuest", 2 },
    ["Trainee"]               = { "MarineQuest", 1 },
    ["Chief Petty Officer"]   = { "MarineQuest", 2 },
    ["Sky Bandit"]            = { "SkyQuest", 1 },
    ["Dark Master"]           = { "SkyQuest", 2 },
    ["Prisoner"]              = { "PrisonerQuest", 1 },
    ["Dangerous Prisoner"]    = { "PrisonerQuest", 2 },
    ["Toga Warrior"]          = { "ColosseumQuest", 1 },
    ["Gladiator"]             = { "ColosseumQuest", 2 },
    ["Military Soldier"]      = { "MagmaQuest", 1 },
    ["Military Spy"]          = { "MagmaQuest", 2 },
    ["Fishman Warrior"]       = { "FishmanQuest", 1 },
    ["Fishman Commando"]      = { "FishmanQuest", 2 },
    ["God's Guard"]           = { "SkyExp1Quest", 1 },
    ["Shanda"]                = { "SkyExp1Quest", 2 },
    ["Royal Squad"]           = { "SkyExp2Quest", 1 },
    ["Royal Soldier"]         = { "SkyExp2Quest", 2 },
    ["Galley Pirate"]         = { "FountainQuest", 1 },
    ["Galley Captain"]        = { "FountainQuest", 2 },
    ["Raider"]                = { "Area1Quest", 1 },
    ["Mercenary"]             = { "Area1Quest", 2 },
    ["Swan Pirate"]           = { "Area2Quest", 1 },
    ["Factory Staff"]         = { "Area2Quest", 2 },
    ["Marine Lieutenant"]     = { "MarineQuest3", 1 },
    ["Marine Captain"]        = { "MarineQuest3", 2 },
    ["Zombie"]                = { "ZombieQuest", 1 },
    ["Vampire"]               = { "ZombieQuest", 2 },
    ["Snow Trooper"]          = { "SnowMountainQuest", 1 },
    ["Winter Warrior"]        = { "SnowMountainQuest", 2 },
    ["Lab Subordinate"]       = { "IceSideQuest", 1 },
    ["Horned Warrior"]        = { "IceSideQuest", 2 },
    ["Magma Ninja"]           = { "FireSideQuest", 1 },
    ["Lava Pirate"]           = { "FireSideQuest", 2 },
    ["Ship Deckhand"]         = { "ShipQuest1", 1 },
    ["Ship Engineer"]         = { "ShipQuest1", 2 },
    ["Ship Steward"]          = { "ShipQuest2", 1 },
    ["Ship Officer"]          = { "ShipQuest2", 2 },
    ["Arctic Warrior"]        = { "FrostQuest", 1 },
    ["Snow Lurker"]           = { "FrostQuest", 2 },
    ["Sea Soldier"]           = { "ForgottenQuest", 1 },
    ["Water Fighter"]         = { "ForgottenQuest", 2 },
    ["Pirate Millionaire"]    = { "PiratePortQuest", 1 },
    ["Pistol Billionaire"]    = { "PiratePortQuest", 2 },
    ["Dragon Crew Warrior"]   = { "AmazonQuest", 1 },
    ["Dragon Crew Archer"]    = { "AmazonQuest", 2 },
    ["Female Islander"]       = { "AmazonQuest2", 1 },
    ["Giant Islander"]        = { "AmazonQuest2", 2 },
    ["Marine Commodore"]      = { "MarineTreeIsland", 1 },
    ["Marine Rear Admiral"]   = { "MarineTreeIsland", 2 },
    ["Fishman Raider"]        = { "DeepForestIsland3", 1 },
    ["Fishman Captain"]       = { "DeepForestIsland3", 2 },
    ["Forest Pirate"]         = { "DeepForestIsland", 1 },
    ["Mythological Pirate"]   = { "DeepForestIsland", 2 },
    ["Jungle Pirate"]         = { "DeepForestIsland2", 1 },
    ["Musketeer Pirate"]      = { "DeepForestIsland2", 2 },
    ["Reborn Skeleton"]       = { "HauntedQuest1", 1 },
    ["Living Zombie"]         = { "HauntedQuest1", 2 },
    ["Demonic Soul"]          = { "HauntedQuest2", 1 },
    ["Posessed Mummy"]        = { "HauntedQuest2", 2 },
    ["Peanut Scout"]          = { "NutsIslandQuest", 1 },
    ["Peanut President"]      = { "NutsIslandQuest", 2 },
    ["Ice Cream Chef"]        = { "IceCreamIslandQuest", 1 },
    ["Ice Cream Commander"]   = { "IceCreamIslandQuest", 2 },
    ["Cookie Crafter"]        = { "CakeQuest1", 1 },
    ["Cake Guard"]            = { "CakeQuest1", 2 },
    ["Baking Staff"]          = { "CakeQuest2", 1 },
    ["Head Baker"]            = { "CakeQuest2", 2 },
    ["Cocoa Warrior"]         = { "ChocQuest1", 1 },
    ["Chocolate Bar Battler"] = { "ChocQuest1", 2 },
    ["Sweet Thief"]           = { "ChocQuest2", 1 },
    ["Candy Rebel"]           = { "ChocQuest2", 2 },
    ["Candy Pirate"]          = { "CandyQuest1", 1 },
    ["Snow Demon"]            = { "CandyQuest1", 2 },
    ["Isle Outlaw"]           = { "TikiQuest1", 1 },
    ["Island Boy"]            = { "TikiQuest1", 2 },
    ["Sun-kissed Warrior"]    = { "TikiQuest2", 1 },
    ["Isle Champion"]         = { "TikiQuest2", 2 },
    ["Serpent Hunter"]        = { "TikiQuest3", 1 },
    ["Skull Slayer"]          = { "TikiQuest3", 2 },
    ["Reef Bandit"]           = { "SubmergedQuest1", 1 },
    ["Coral Pirate"]          = { "SubmergedQuest1", 2 },
    ["Sea Chanter"]           = { "SubmergedQuest2", 1 },
    ["Ocean Prophet"]         = { "SubmergedQuest2", 2 },
    ["High Disciple"]         = { "SubmergedQuest3", 1 },
    ["Grand Devotee"]         = { "SubmergedQuest3", 2 },
}
P.quests = QUESTS

local GIVER_POS = {
    ["Raider"]                = Vector3.new(-427.7, 73.0, 1835.9),
    ["Mercenary"]             = Vector3.new(-427.7, 73.0, 1835.9),
    ["Swan Pirate"]           = Vector3.new(635.6, 73.1, 917.8),
    ["Factory Staff"]         = Vector3.new(635.6, 73.1, 917.8),
    ["Marine Lieutenant"]     = Vector3.new(-2441.0, 73.0, -3217.7),
    ["Marine Captain"]        = Vector3.new(-2441.0, 73.0, -3217.7),
    ["Zombie"]                = Vector3.new(-5494.3, 48.5, -794.6),
    ["Vampire"]               = Vector3.new(-5494.3, 48.5, -794.6),
    ["Snow Trooper"]          = Vector3.new(607.1, 401.5, -5370.6),
    ["Winter Warrior"]        = Vector3.new(607.1, 401.5, -5370.6),
    ["Lab Subordinate"]       = Vector3.new(-6061.8, 15.9, -4902.0),
    ["Horned Warrior"]        = Vector3.new(-6061.8, 15.9, -4902.0),
    ["Magma Ninja"]           = Vector3.new(-5429.1, 16.0, -5298.0),
    ["Lava Pirate"]           = Vector3.new(-5429.1, 16.0, -5298.0),
    ["Ship Deckhand"]         = Vector3.new(1040.3, 125.1, 32911.0),
    ["Ship Engineer"]         = Vector3.new(1040.3, 125.1, 32911.0),
    ["Ship Steward"]          = Vector3.new(971.4, 125.1, 33245.5),
    ["Ship Officer"]          = Vector3.new(971.4, 125.1, 33245.5),
    ["Arctic Warrior"]        = Vector3.new(5668.1, 28.2, -6484.6),
    ["Snow Lurker"]           = Vector3.new(5668.1, 28.2, -6484.6),
    ["Sea Soldier"]           = Vector3.new(-3054.6, 236.9, -10147.8),
    ["Water Fighter"]         = Vector3.new(-3054.6, 236.9, -10147.8),
    ["Pirate Millionaire"]    = Vector3.new(-290.1, 42.9, 5581.6),
    ["Pistol Billionaire"]    = Vector3.new(-290.1, 42.9, 5581.6),
    ["Dragon Crew Warrior"]   = Vector3.new(5832.8, 51.7, -1101.5),
    ["Dragon Crew Archer"]    = Vector3.new(5832.8, 51.7, -1101.5),
    ["Female Islander"]       = Vector3.new(5448.9, 601.5, 751.1),
    ["Giant Islander"]        = Vector3.new(5448.9, 601.5, 751.1),
    ["Marine Commodore"]      = Vector3.new(2180.5, 27.8, -6741.6),
    ["Marine Rear Admiral"]   = Vector3.new(2180.5, 27.8, -6741.6),
    ["Fishman Raider"]        = Vector3.new(-10581.7, 330.9, -8761.2),
    ["Fishman Captain"]       = Vector3.new(-10581.7, 330.9, -8761.2),
    ["Forest Pirate"]         = Vector3.new(-13234.0, 331.5, -7625.4),
    ["Mythological Pirate"]   = Vector3.new(-13234.0, 331.5, -7625.4),
    ["Jungle Pirate"]         = Vector3.new(-12680.4, 390.0, -9902.0),
    ["Musketeer Pirate"]      = Vector3.new(-12680.4, 390.0, -9902.0),
    ["Reborn Skeleton"]       = Vector3.new(-9480.8, 142.1, 5566.1),
    ["Living Zombie"]         = Vector3.new(-9480.8, 142.1, 5566.1),
    ["Demonic Soul"]          = Vector3.new(-9517.0, 178.0, 6078.5),
    ["Posessed Mummy"]        = Vector3.new(-9517.0, 178.0, 6078.5),
    ["Peanut Scout"]          = Vector3.new(-2104.4, 38.1, -10194.1),
    ["Peanut President"]      = Vector3.new(-2104.4, 38.1, -10194.1),
    ["Ice Cream Chef"]        = Vector3.new(-820.2, 65.8, -10966.2),
    ["Ice Cream Commander"]   = Vector3.new(-820.2, 65.8, -10966.2),
    ["Cookie Crafter"]        = Vector3.new(-2022.3, 36.9, -12030.9),
    ["Cake Guard"]            = Vector3.new(-2022.3, 36.9, -12030.9),
    ["Baking Staff"]          = Vector3.new(-1928.3, 37.7, -12840.6),
    ["Head Baker"]            = Vector3.new(-1928.3, 37.7, -12840.6),
    ["Cocoa Warrior"]         = Vector3.new(231.8, 23.9, -12200.3),
    ["Chocolate Bar Battler"] = Vector3.new(231.8, 23.9, -12200.3),
    ["Sweet Thief"]           = Vector3.new(151.2, 23.9, -12774.6),
    ["Candy Rebel"]           = Vector3.new(151.2, 23.9, -12774.6),
    ["Candy Pirate"]          = Vector3.new(-1149.3, 13.6, -14445.6),
    ["Snow Demon"]            = Vector3.new(-1149.3, 13.6, -14445.6),
    ["Isle Outlaw"]           = Vector3.new(-16549.9, 55.7, -179.9),
    ["Island Boy"]            = Vector3.new(-16549.9, 55.7, -179.9),
    ["Sun-kissed Warrior"]    = Vector3.new(-16541.0, 54.8, 1051.5),
    ["Isle Champion"]         = Vector3.new(-16541.0, 54.8, 1051.5),
    ["Serpent Hunter"]        = Vector3.new(-16665.2, 104.6, 1579.7),
    ["Skull Slayer"]          = Vector3.new(-16665.2, 104.6, 1579.7),
    ["Reef Bandit"]           = Vector3.new(10780.1, -2087.7, 9261.9),
    ["Coral Pirate"]          = Vector3.new(10780.1, -2087.7, 9261.9),
    ["Sea Chanter"]           = Vector3.new(10883.6, -2086.2, 10032.2),
    ["Ocean Prophet"]         = Vector3.new(10883.6, -2086.2, 10032.2),
    ["High Disciple"]         = Vector3.new(9635.9, -1992.4, 9614.4),
    ["Grand Devotee"]         = Vector3.new(9635.9, -1992.4, 9614.4),
}
P.giverPositions = GIVER_POS

local GIVER_NAMES = {
    ["Bandit"]                = "Bandit Quest Giver",
    ["Monkey"]                = "Adventurer",
    ["Gorilla"]               = "Adventurer",
    ["Pirate"]                = "Pirate Adventurer",
    ["Brute"]                 = "Pirate Adventurer",
    ["Desert Bandit"]         = "Desert Adventurer",
    ["Desert Officer"]        = "Desert Adventurer",
    ["Snow Bandit"]           = "Villager",
    ["Snowman"]               = "Villager",
    ["Chief Petty Officer"]   = "Marine",
    ["Sky Bandit"]            = "Sky Adventurer",
    ["Dark Master"]           = "Sky Adventurer",
    ["Prisoner"]              = "Jail Keeper",
    ["Dangerous Prisoner"]    = "Jail Keeper",
    ["Toga Warrior"]          = "Colosseum Quest Giver",
    ["Gladiator"]             = "Colosseum Quest Giver",
    ["God's Guard"]           = "Sky Quest Giver 2",
    ["Shanda"]                = "Sky Quest Giver 2",
    ["Royal Squad"]           = "Mole",
    ["Royal Soldier"]         = "Mole",
    ["Raider"]                = "Area 1 Quest Giver",
    ["Mercenary"]             = "Area 1 Quest Giver",
    ["Swan Pirate"]           = "Area 2 Quest Giver",
    ["Factory Staff"]         = "Area 2 Quest Giver",
    ["Marine Lieutenant"]     = "Marine Quest Giver",
    ["Marine Captain"]        = "Marine Quest Giver",
    ["Zombie"]                = "Graveyard Quest Giver",
    ["Vampire"]               = "Graveyard Quest Giver",
    ["Snow Trooper"]          = "Snow Quest Giver",
    ["Winter Warrior"]        = "Snow Quest Giver",
    ["Lab Subordinate"]       = "Ice Quest Giver",
    ["Horned Warrior"]        = "Ice Quest Giver",
    ["Magma Ninja"]           = "Fire Quest Giver",
    ["Lava Pirate"]           = "Fire Quest Giver",
    ["Sea Soldier"]           = "Forgotten Quest Giver",
    ["Water Fighter"]         = "Forgotten Quest Giver",
    ["Ship Deckhand"]         = "Front Crew Quest Giver",
    ["Ship Engineer"]         = "Front Crew Quest Giver",
    ["Ship Steward"]          = "Rear Crew Quest Giver",
    ["Ship Officer"]          = "Rear Crew Quest Giver",
    ["Arctic Warrior"]        = "Frost Quest Giver",
    ["Snow Lurker"]           = "Frost Quest Giver",
    ["Pirate Millionaire"]    = "Port Town Quest Giver",
    ["Pistol Billionaire"]    = "Port Town Quest Giver",
    ["Dragon Crew Warrior"]   = "Hydra Town Quest Giver",
    ["Dragon Crew Archer"]    = "Hydra Town Quest Giver",
    ["Female Islander"]       = "Hydra Island Quest Giver",
    ["Giant Islander"]        = "Hydra Island Quest Giver",
    ["Marine Commodore"]      = "Marine Tree Quest Giver",
    ["Marine Rear Admiral"]   = "Marine Tree Quest Giver",
    ["Fishman Raider"]        = "Deep Forest Quest Giver 3",
    ["Fishman Captain"]       = "Deep Forest Quest Giver 3",
    ["Forest Pirate"]         = "Deep Forest Quest Giver",
    ["Mythological Pirate"]   = "Deep Forest Quest Giver",
    ["Jungle Pirate"]         = "Deep Forest Quest Giver 2",
    ["Musketeer Pirate"]      = "Deep Forest Quest Giver 2",
    ["Reborn Skeleton"]       = "Haunted Castle Quest Giver 1",
    ["Living Zombie"]         = "Haunted Castle Quest Giver 1",
    ["Demonic Soul"]          = "Haunted Castle Quest Giver 2",
    ["Posessed Mummy"]        = "Haunted Castle Quest Giver 2",
    ["Peanut Scout"]          = "Peanut Quest Giver",
    ["Peanut President"]      = "Peanut Quest Giver",
    ["Ice Cream Chef"]        = "Ice Cream Quest Giver",
    ["Ice Cream Commander"]   = "Ice Cream Quest Giver",
    ["Cookie Crafter"]        = "Cake Quest Giver 1",
    ["Cake Guard"]            = "Cake Quest Giver 1",
    ["Baking Staff"]          = "Cake Quest Giver 2",
    ["Head Baker"]            = "Cake Quest Giver 2",
    ["Cocoa Warrior"]         = "Chocolate Quest Giver 1",
    ["Chocolate Bar Battler"] = "Chocolate Quest Giver 1",
    ["Sweet Thief"]           = "Chocolate Quest Giver 2",
    ["Candy Rebel"]           = "Chocolate Quest Giver 2",
    ["Candy Pirate"]          = "Candy Cane Quest Giver",
    ["Snow Demon"]            = "Candy Cane Quest Giver",
    ["Isle Outlaw"]           = "Tiki Quest Giver 1",
    ["Island Boy"]            = "Tiki Quest Giver 1",
    ["Sun-kissed Warrior"]    = "Tiki Quest Giver 2",
    ["Isle Champion"]         = "Tiki Quest Giver 2",
    ["Serpent Hunter"]        = "Tiki Quest Giver 3",
    ["Skull Slayer"]          = "Tiki Quest Giver 3",
    ["Reef Bandit"]           = "Submerged Quest Giver 1",
    ["Coral Pirate"]          = "Submerged Quest Giver 1",
    ["Sea Chanter"]           = "Submerged Quest Giver 2",
    ["Ocean Prophet"]         = "Submerged Quest Giver 2",
    ["High Disciple"]         = "Submerged Quest Giver 3",
    ["Grand Devotee"]         = "Submerged Quest Giver 3",
}
P.giverNames = GIVER_NAMES

local KNOWN_GIVERS = {}
for _, n in ipairs({
    "Bandit Quest Giver", "Adventurer", "Pirate Adventurer", "Desert Adventurer",
    "Villager", "Marine", "Marine Leader", "Colosseum Quest Giver",
    "Sky Adventurer", "Sky Quest Giver 2", "Mole", "Head Jailer", "Jail Keeper",
    "Freezeburg Quest Giver", "Submerged Quest Giver 1", "Submerged Quest Giver 2",
    "Area 1 Quest Giver", "Area 2 Quest Giver", "Marine Quest Giver",
    "Graveyard Quest Giver", "Snow Quest Giver", "Ice Quest Giver",
    "Fire Quest Giver", "Forgotten Quest Giver", "Front Crew Quest Giver",
    "Rear Crew Quest Giver", "Frost Quest Giver",
    "Port Town Quest Giver", "Pirate Port Quest Giver", "Hydra Town Quest Giver",
    "Hydra Island Quest Giver", "Dragon Crew Quest Giver",
    "Marine Tree Quest Giver", "Turtle Adventure Quest Giver",
    "Deep Forest Quest Giver", "Deep Forest Quest Giver 2",
    "Deep Forest Quest Giver 3", "Haunted Castle Quest Giver 1",
    "Haunted Castle Quest Giver 2", "Cake Quest Giver 1", "Cake Quest Giver 2",
    "Chocolate Quest Giver 1", "Chocolate Quest Giver 2", "Ice Cream Quest Giver",
    "Peanut Quest Giver", "Candy Cane Quest Giver", "Submerged Quest Giver 3",
    "Tiki Quest Giver 1", "Tiki Quest Giver 2", "Tiki Quest Giver 3",
}) do KNOWN_GIVERS[string.lower(n)] = n end
P.knownGivers = KNOWN_GIVERS

local stats = {
    kills = 0, swings = 0, damaging = 0, quests = 0,
    escalations = 0, retreats = 0, walks = 0, dashes = 0, startedAt = 0,
    switches = 0, hops = 0, airJumps = 0,
    panics = 0, panicDashes = 0, detours = 0, hakiPresses = 0,
    gathers = 0, tagged = 0, ghosts = 0, lifts = 0, ghostFalls = 0,
    navMaps = 0, navPlans = 0, navJumps = 0, navLearned = 0, navClimbs = 0,
}

local state          = "IDLE"
local statusLine     = "idle"
local stateEnteredAt = 0
local lastProgressAt = 0
local escalation     = 0
local blacklist      = {}
local countedDead    = {}
local conns          = {}
local moveEnabled    = true
local waterFloor     = nil

local activeName     = nil
local farmSpot       = nil
local engagedModel   = nil
local pathUntil      = 0
local lastJumpAt     = 0

P.learnedGivers = {}
P.learnedQuests = {}
P.giverSpots    = {}
P.lockedQuest   = nil

local epoch = 0
local function stale(e) return e ~= epoch end

local function track(c) table.insert(conns, c) return c end
local function log(m) if CFG.Debug then print("[BFP] " .. tostring(m)) end end
local function say(s) statusLine = tostring(s) end

local function setState(s)
    if state ~= s then
        state = s
        stateEnteredAt = os.clock()
        log("state -> " .. s)
    end
end

local function progress()
    lastProgressAt = os.clock()
    escalation = 0
end

local function jitter(lo, hi)
    if hi <= lo then return lo end
    return lo + math.random() * (hi - lo)
end

local function parts()
    local char = player.Character
    if not char then return nil end
    local root = char:FindFirstChild("HumanoidRootPart")
    local hum  = char:FindFirstChildOfClass("Humanoid")
    if not root or not hum or hum.Health <= 0 then return char, nil, nil end
    return char, root, hum
end

local function healthPct()
    local _, _, hum = parts()
    if not hum or hum.MaxHealth <= 0 then return 1 end
    return hum.Health / hum.MaxHealth
end

local function playerLevel()
    local ls = player:FindFirstChild("leaderstats")
    local lv = ls and ls:FindFirstChild("Level")
    if lv and tonumber(lv.Value) then return tonumber(lv.Value) end
    local d = player:FindFirstChild("Data")
    local l2 = d and d:FindFirstChild("Level")
    return l2 and tonumber(l2.Value) or nil
end

local function toolNames()
    local out, seen = {}, {}
    local bp = player:FindFirstChild("Backpack")
    for _, src in ipairs({ bp, player.Character }) do
        if src then
            for _, t in ipairs(src:GetChildren()) do
                if t:IsA("Tool") and not seen[t.Name] then
                    seen[t.Name] = true
                    table.insert(out, t.Name)
                end
            end
        end
    end
    table.sort(out)
    return out
end
P.tools = toolNames

local function heldTool()
    local char = player.Character
    return char and char:FindFirstChildOfClass("Tool")
end
P.heldTool = function()
    local t = heldTool()
    return t and t.Name or nil
end

local lastHeld = nil
local function keepWeapon()
    local want = CFG.Weapon
    if not want or want == "" then
        local t = heldTool()
        if t then lastHeld = t.Name; P.lastHeld = lastHeld end
        return t and t.Name or nil
    end
    local t = heldTool()
    if t and t.Name == want then return want end

    local char = player.Character
    local bp   = player:FindFirstChild("Backpack")
    local tool = (bp and bp:FindFirstChild(want)) or (char and char:FindFirstChild(want))
    if tool and tool:IsA("Tool") then
        local hum = char and char:FindFirstChildOfClass("Humanoid")
        if hum then pcall(function() hum:EquipTool(tool) end) end
        return want
    end
    return t and t.Name or nil
end

local fastConn, ctrlRef = nil, nil
local lastCleared = 0
P.fastOK = false

local function installFastAttack()
    if fastConn then pcall(function() fastConn:Disconnect() end) fastConn = nil end
    ctrlRef, P.fastOK = nil, false

    local env     = (getgenv and getgenv()) or {}
    local getreg_ = getreg or env.getreg
    local getupv  = (debug and debug.getupvalues) or env.getupvalues
    if not getreg_ or not getupv then
        P.fastNote = "not available: this executor has no getreg/getupvalues"
        return false
    end

    local scripts = player:FindFirstChild("PlayerScripts")
    local combatScript = scripts and scripts:FindFirstChild("CombatFramework")
    if not combatScript then
        P.fastNote = "not available: CombatFramework missing"
        return false
    end

    local found
    pcall(function()
        for _, v in pairs(getreg_()) do
            if typeof(v) == "function" then
                local okE, fenv = pcall(getfenv, v)
                if okE and fenv and rawget(fenv, "script") == combatScript then
                    local okU, ups = pcall(getupv, v)
                    if okU and ups then
                        for _, up in pairs(ups) do
                            if typeof(up) == "table" and rawget(up, "activeController") ~= nil then
                                found = up
                                return
                            end
                        end
                    end
                end
            end
        end
    end)

    if not found then
        P.fastNote = "not available: activeController not found"
        return false
    end

    ctrlRef  = found
    P.fastOK = true
    P.fastNote = "installed"
    fastConn = track(RunService.RenderStepped:Connect(function()
        if not CFG.FastAttack then return end
        local gap = math.max(CFG.AttackSpeed or 0.35, 0.05)
        if os.clock() - lastCleared < gap then return end
        lastCleared = os.clock()
        pcall(function()
            local ac = ctrlRef.activeController
            if not ac then return end
            ac.timeToNextAttack   = 0
            ac.attacking          = false
            ac.blocking           = false
            ac.focusStart         = 0
            ac.currentAttackTrack = 0
        end)
    end))
    return true
end
P.installFastAttack = installFastAttack

local swingIndex = 0

local function pressM1()
    local cam = workspace.CurrentCamera
    if not cam then return end
    local vs = cam.ViewportSize
    local x, y = vs.X * 0.5, vs.Y * 0.5

    pcall(function() VIM:SendMouseButtonEvent(x, y, 0, true, game, 0) end)
    task.wait(0.04)
    pcall(function() VIM:SendMouseButtonEvent(x, y, 0, false, game, 0) end)

    pcall(function()
        VirtualUser:CaptureController()
        VirtualUser:Button1Down(Vector2.new(x, y), cam.CFrame)
        VirtualUser:Button1Up(Vector2.new(x, y), cam.CFrame)
    end)
end

local function pressKey(code)
    pcall(function()
        VIM:SendKeyEvent(true, code, false, game)
        task.wait(0.04)
        VIM:SendKeyEvent(false, code, false, game)
    end)
end

local function jump()
    local _, _, h = parts()
    if h then pcall(function() h.Jump = true end) end
    task.spawn(pressKey, Enum.KeyCode.Space)
end

local function rayHit(r, dir, len, yOff)
    local excl = {}
    local char = player.Character
    if char then table.insert(excl, char) end
    local enemies = workspace:FindFirstChild("Enemies")
    if enemies then table.insert(excl, enemies) end
    if waterFloor then table.insert(excl, waterFloor) end
    local ok, hit = pcall(function()
        local params = RaycastParams.new()
        params.FilterType = Enum.RaycastFilterType.Exclude
        params.FilterDescendantsInstances = excl
        params.RespectCanCollide = true
        local origin = r.Position + Vector3.new(0, yOff, 0)
        return workspace:Raycast(origin, dir * len, params)
    end)
    return ok and hit ~= nil
end

local function ledgeAhead(r, h)
    local md = h.MoveDirection
    if md.Magnitude < 0.1 then return false end
    if h.FloorMaterial == Enum.Material.Air then return false end
    return rayHit(r, md.Unit, 4.5, -1.5)
end

local lastSide = 1
local function openSide(r, dir)
    local right = Vector3.new(-dir.Z, 0, dir.X)
    local rOpen = not rayHit(r, right, 10, 2)
    local lOpen = not rayHit(r, -right, 10, 2)
    if rOpen and not lOpen then return 1 end
    if lOpen and not rOpen then return -1 end
    return lastSide
end

local ghosting    = false
local ghostSince  = 0
local ghostWhy    = ""
local ghostGen    = 0
local ghostOrig   = {}
local ghostConn   = nil
local ghostLifts  = 0
local lastLiftAt  = 0
local lastClearAt = 0
local ghostFrom   = nil
local ghostQuietUntil = 0
local blockAt, blockPos = nil, nil
local chaseGoal, chaseGoalAt = nil, 0
local function setChase(pos) chaseGoal, chaseGoalAt = pos, os.clock() end

local function charParts(char)
    local out = {}
    for _, d in ipairs(char:GetDescendants()) do
        if d:IsA("BasePart") then table.insert(out, d) end
    end
    return out
end

local function ghostOff()
    if ghostConn then pcall(function() ghostConn:Disconnect() end) ghostConn = nil end
    if not ghosting then return end
    ghosting = false
    for part, was in pairs(ghostOrig) do
        if part.Parent then pcall(function() part.CanCollide = was end) end
    end
    table.clear(ghostOrig)
end
P.ghostOff = ghostOff
P.ghosting = function() return ghosting, ghostWhy end

local function bodyClear(char)
    local excl = {}
    for _, pl in ipairs(Players:GetPlayers()) do
        if pl.Character then table.insert(excl, pl.Character) end
    end
    local enemies = workspace:FindFirstChild("Enemies")
    if enemies then table.insert(excl, enemies) end
    if waterFloor then table.insert(excl, waterFloor) end
    local op = OverlapParams.new()
    op.FilterType = Enum.RaycastFilterType.Exclude
    op.FilterDescendantsInstances = excl
    op.RespectCanCollide = true
    for _, n in ipairs({ "HumanoidRootPart", "UpperTorso", "Torso", "Head" }) do
        local p = char:FindFirstChild(n)
        if p and p:IsA("BasePart") then
            local ok, hits = pcall(function() return workspace:GetPartsInPart(p, op) end)
            if ok and hits and #hits > 0 then return false end
        end
    end
    return true
end

local function ghostOn(why)
    if not CFG.Ghost then return end
    local char = player.Character
    if not char then return end
    ghostGen += 1
    ghostSince, ghostWhy, ghostLifts = os.clock(), why or "blocked", 0
    say("ghost - " .. ghostWhy)
    if ghosting then return end
    local root = char:FindFirstChild("HumanoidRootPart")
    ghostFrom = root and root.Position or nil
    ghosting = true
    stats.ghosts += 1
    local list, listAt = charParts(char), os.clock()
    ghostConn = RunService.Stepped:Connect(function()
        if player.Character ~= char then ghostOff() return end
        if os.clock() - listAt > 0.5 then list, listAt = charParts(char), os.clock() end
        for _, p in ipairs(list) do
            if ghostOrig[p] == nil then ghostOrig[p] = p.CanCollide end
            p.CanCollide = false
        end
    end)
end

local function ghostWatch()
    local char, r, h = parts()
    if not char or not r or not h then blockAt = nil return end
    local now = os.clock()

    if ghosting then
        local g = (chaseGoal and now - chaseGoalAt < 0.5) and chaseGoal
            or (h.WalkToPoint + Vector3.new(0, 3, 0))

        if ghostFrom and r.Position.Y < ghostFrom.Y - 10 and r.Position.Y < g.Y - 4 then
            local back = ghostFrom + Vector3.new(0, 2, 0)
            ghostOff()
            pcall(function()
                r.AssemblyLinearVelocity = Vector3.zero
                r.CFrame = CFrame.new(back) * (r.CFrame - r.CFrame.Position)
            end)
            ghostQuietUntil, blockAt = now + 10, nil
            stats.ghostFalls += 1
            say("ghost fell through - back, trying the long way")
            return
        end

        if CFG.Ghost and P.running and h.MoveDirection.Magnitude > 0.1
            and ghostLifts < 3 and now - lastLiftAt > 1.2 then
            local rise = g.Y - r.Position.Y
            if rise > 4 then
                lastLiftAt = now
                ghostLifts += 1
                stats.lifts += 1
                local height = math.clamp(rise + 5, 6, CFG.GhostLiftMax or 30)
                local vy = math.sqrt(2 * workspace.Gravity * height)
                pcall(function() h:ChangeState(Enum.HumanoidStateType.Jumping) end)
                local v = r.AssemblyLinearVelocity
                r.AssemblyLinearVelocity = Vector3.new(v.X, vy, v.Z)
                ghostSince = now
                say(string.format("ghost - lifting %.0f studs", height))
            end
        end
        if now - ghostSince > 1.5 and now - lastClearAt > 0.2 then
            lastClearAt = now
            if bodyClear(char) then
                ghostOff()
                blockAt = nil
                say("through")
            end
        end
        return
    end

    if not P.running or not CFG.Ghost or not moveEnabled or now < ghostQuietUntil then
        blockAt = nil
        return
    end
    local md = h.MoveDirection
    local dir = Vector3.new(md.X, 0, md.Z)
    if dir.Magnitude < 0.1 or h.WalkSpeed < 2 or r.Anchored then blockAt = nil return end
    dir = dir.Unit
    if not blockAt then blockAt, blockPos = now, r.Position return end
    local moved = r.Position - blockPos
    if Vector3.new(moved.X, 0, moved.Z):Dot(dir) >= 3 then
        blockAt, blockPos = now, r.Position
    elseif now - blockAt >= (CFG.GhostAfter or 1.5) then
        blockAt = nil
        ghostOn("blocked, going through")
    end
end

local function ghostRelease()
    if not ghosting then ghostOff() return end
    local gen = ghostGen
    task.spawn(function()
        local t0 = os.clock()
        while ghosting and os.clock() - t0 < 5 do
            local c = player.Character
            if not c or bodyClear(c) then break end
            task.wait(0.2)
        end
        if ghostGen == gen then ghostOff() end
    end)
end

local WATER_Y = 112
P.waterNote = "not looked yet"
P.waterSets = 0

local function keepWater()
    local map = workspace:FindFirstChild("Map")
    local wp = map and map:FindFirstChild("WaterBase-Plane")
    if not (wp and wp:IsA("BasePart")) then
        P.waterNote = "no WaterBase-Plane in workspace.Map here"
        return
    end
    if math.abs(wp.Size.Y - WATER_Y) > 0.5 then
        wp.Size = Vector3.new(wp.Size.X, WATER_Y, wp.Size.Z)
        P.waterSets += 1
    end
    P.waterNote = "solid - standing on the surface"
end

local DEEP_Y = -1000
local deepNote = "not down there"
local deepSurf, deepSurfAt, deepLiftAt = nil, 0, 0
local slabOrig = {}
P.deepLifts = 0
P.deepNote = function() return deepNote end

local function deepExcl()
    local excl = {}
    for _, pl in ipairs(Players:GetPlayers()) do
        if pl.Character then table.insert(excl, pl.Character) end
    end
    local enemies = workspace:FindFirstChild("Enemies")
    if enemies then table.insert(excl, enemies) end
    if waterFloor then table.insert(excl, waterFloor) end
    return excl
end

local function terrainWaterTop(x, z, yLo, yHi)
    local region = Region3.new(Vector3.new(x - 2, yLo, z - 2),
        Vector3.new(x + 2, yHi, z + 2)):ExpandToGrid(4)
    local mats, occs = workspace.Terrain:ReadVoxels(region, 4)
    local sz = mats.Size
    local minY = region.CFrame.Position.Y - region.Size.Y / 2
    for iy = sz.Y, 1, -1 do
        for ix = 1, sz.X do
            for iz = 1, sz.Z do
                if mats[ix][iy][iz] == Enum.Material.Water then
                    return minY + (iy - 1) * 4 + 4 * math.min(1, occs[ix][iy][iz] or 1),
                        iy == sz.Y
                end
            end
        end
    end
    return nil
end

local function partWater(pos, yLo, yHi)
    local op = OverlapParams.new()
    op.FilterType = Enum.RaycastFilterType.Exclude
    op.FilterDescendantsInstances = deepExcl()
    op.RespectCanCollide = false
    local hits = workspace:GetPartBoundsInBox(CFrame.new(pos.X, (yLo + yHi) / 2, pos.Z),
        Vector3.new(4, yHi - yLo, 4), op)
    local top, slab = nil, nil
    for _, part in ipairs(hits) do
        local n = string.lower(part.Name)
        if string.find(n, "waterbase", 1, true) then
            slab = slab or part
        elseif not part.CanCollide and (string.find(n, "water", 1, true)
            or part.Material == Enum.Material.Water) then
            local t = part.Position.Y + part.Size.Y / 2
            if t <= yHi and (not top or t > top) then top = t end
        end
    end
    return top, slab
end

local function parkFloor()
    if waterFloor and waterFloor.Parent then waterFloor.Parent = nil end
end

local function deepTick()
    local _, r, h = parts()
    if not r or not h then parkFloor() return end
    local pos, now = r.Position, os.clock()
    if pos.Y > DEEP_Y then
        parkFloor()
        deepSurf, deepNote = nil, "not down there"
        return
    end

    if now - deepSurfAt > 0.1 then
        deepSurfAt = now
        local yLo, yHi = pos.Y - 60, pos.Y + 12
        local okT, tw, capped = pcall(terrainWaterTop, pos.X, pos.Z, yLo, yHi)
        if not okT then tw, capped = nil, false end
        local climbs = 0
        while tw and capped and climbs < 4 do
            climbs += 1
            local ok2, t2, c2 = pcall(terrainWaterTop, pos.X, pos.Z, tw - 4, tw + 64)
            if not ok2 or not t2 then break end
            tw, capped = t2, c2
        end
        if tw and capped then tw = nil end
        local okP, pw, slab = pcall(partWater, pos, yLo, yHi)
        if not okP then pw, slab = nil, nil end
        if slab then
            local o = slabOrig[slab] or slab.Size.Y
            slabOrig[slab] = o
            if math.abs(slab.Size.Y - (o + 32)) > 0.5 then
                slab.Size = Vector3.new(slab.Size.X, o + 32, slab.Size.Z)
            end
        end
        deepSurf = tw or pw
        if tw and pw then deepSurf = math.max(tw, pw) end
        if deepSurf then
            deepNote = string.format("%s at Y %.0f - standing on it",
                tw and "terrain water" or ("water part"), deepSurf)
        elseif slab then
            deepNote = "deep floor slab '" .. slab.Name .. "' raised"
        else
            deepNote = "no water under you here"
        end
    end
    if not deepSurf then parkFloor() return end

    if not waterFloor then
        local f = Instance.new("Part")
        f.Name = "BFP_WaterFloor"
        f.Anchored, f.CanCollide, f.CanTouch = true, true, false
        f.Transparency = 1
        f.Size = Vector3.new(24, 1, 24)
        waterFloor = f
    end
    waterFloor.CFrame = CFrame.new(pos.X, deepSurf - 0.5, pos.Z)
    if waterFloor.Parent ~= workspace then waterFloor.Parent = workspace end

    local feet = pos.Y - (h.HipHeight + r.Size.Y / 2)
    if feet < deepSurf - 0.75 and deepSurf - feet < 300 and now - deepLiftAt > 0.4 then
        deepLiftAt = now
        r.CFrame = r.CFrame + Vector3.new(0, deepSurf - feet + 0.2, 0)
        local v = r.AssemblyLinearVelocity
        r.AssemblyLinearVelocity = Vector3.new(v.X, math.max(v.Y, 0), v.Z)
        P.deepLifts += 1
    end
end

local Nav = {}
local NAV_STEP  = 1.2
local NAV_CLIMB = 40
local NAV_SQ2  = math.sqrt(2)
local NAV_DIRS = {
    {  1,  0, 1, false }, { -1,  0, 1, true },
    {  0,  1, 2, false }, {  0, -1, 2, true },
    {  1,  1, 3, false }, { -1, -1, 3, true },
    { -1,  1, 4, false }, {  1, -1, 4, true },
}
local NAV_FWD = { { 1, 0 }, { 0, 1 }, { 1, 1 }, { -1, 1 } }
local NAV_DIR_OF = { [-1] = {}, [0] = {}, [1] = {} }
for k, e in ipairs(NAV_DIRS) do NAV_DIR_OF[e[1]][e[2]] = k end

function Nav.new(cx, cz, radius, cell)
    local n = math.floor(2 * radius / cell) + 1
    return {
        n = n, C = cell, cx = cx, cz = cz,
        x0 = cx - (n - 1) * cell / 2, z0 = cz - (n - 1) * cell / 2,
        H = {}, body = { {}, {}, {}, {} }, knee = { {}, {}, {}, {} },
        near = {}, learned = 0, ready = false, done = 0, total = 2 * n * n,
    }
end

local function navIdx(m, i, j) return j * m.n + i + 1 end

function Nav.cellOf(m, x, z)
    local i = math.floor((x - m.x0) / m.C + 0.5)
    local j = math.floor((z - m.z0) / m.C + 0.5)
    if i < 0 or j < 0 or i >= m.n or j >= m.n then return nil end
    return i, j
end

function Nav.center(m, i, j) return m.x0 + i * m.C, m.z0 + j * m.C end

local function navSlot(m, i, j, k)
    local e = NAV_DIRS[k]
    local bi, bj = i + e[1], j + e[2]
    if bi < 0 or bj < 0 or bi >= m.n or bj >= m.n then return nil end
    local a, b = navIdx(m, i, j), navIdx(m, bi, bj)
    return e[3], (e[4] and b or a), a, b
end

function Nav.edge(m, i, j, k, jumpMax)
    local d, slot, a, b = navSlot(m, i, j, k)
    if not d then return 2 end
    local hA, hB = m.H[a], m.H[b]
    if not hA or not hB then return 2 end
    if m.body[d][slot] then return 2 end
    local rise = hB - hA
    if rise > jumpMax then
        if rise <= NAV_CLIMB and k <= 4 then return 3 end
        return 2
    end
    if rise > NAV_STEP or m.knee[d][slot] then return 1 end
    return 0
end

function Nav.block(m, i, j, k)
    local d, slot = navSlot(m, i, j, k)
    if d and not m.body[d][slot] then
        m.body[d][slot] = true
        m.learned += 1
    end
end

function Nav.survey(m, yTop, rayDown, rayFlat, budget, pause)
    local n, used = m.n, 0
    local function tick()
        used += 1
        if used < budget then return true end
        used = 0
        return pause()
    end
    for j = 0, n - 1 do
        for i = 0, n - 1 do
            local x, z = Nav.center(m, i, j)
            m.H[navIdx(m, i, j)] = rayDown(x, yTop, z, 400)
            m.done += 1
            if not tick() then return false end
        end
    end
    for j = 0, n - 1 do
        for i = 0, n - 1 do
            local a = navIdx(m, i, j)
            local hA = m.H[a]
            local x1, z1 = Nav.center(m, i, j)
            for d = 1, 4 do
                local bi, bj = i + NAV_FWD[d][1], j + NAV_FWD[d][2]
                if hA and bi >= 0 and bj >= 0 and bi < n and bj < n then
                    local hB = m.H[navIdx(m, bi, bj)]
                    if hB then
                        local x2, z2 = Nav.center(m, bi, bj)
                        local top = math.max(hA, hB)
                        if rayFlat(x1, top + 2.5, z1, x2, z2) then m.body[d][a] = true end
                        if not tick() then return false end
                        if math.abs(hB - hA) <= NAV_STEP then
                            if rayFlat(x1, top + 1.0, z1, x2, z2) then m.knee[d][a] = true end
                            if not tick() then return false end
                        end
                    end
                end
            end
            m.done += 1
        end
    end
    for j = 0, n - 1 do
        for i = 0, n - 1 do
            local c = 0
            for k = 1, 4 do
                if Nav.edge(m, i, j, k, math.huge) == 2 then c += 1 end
            end
            m.near[navIdx(m, i, j)] = c
        end
    end
    m.ready = true
    return true
end

local function navPush(hf, hv, f, v)
    local k = #hf + 1
    hf[k], hv[k] = f, v
    while k > 1 do
        local p = k // 2
        if hf[p] <= hf[k] then break end
        hf[p], hf[k] = hf[k], hf[p]
        hv[p], hv[k] = hv[k], hv[p]
        k = p
    end
end

local function navPop(hf, hv)
    local n = #hf
    local top = hv[1]
    hf[1], hv[1] = hf[n], hv[n]
    hf[n], hv[n] = nil, nil
    n -= 1
    local k = 1
    while true do
        local l, r, s = 2 * k, 2 * k + 1, k
        if l <= n and hf[l] < hf[s] then s = l end
        if r <= n and hf[r] < hf[s] then s = r end
        if s == k then break end
        hf[s], hf[k] = hf[k], hf[s]
        hv[s], hv[k] = hv[k], hv[s]
        k = s
    end
    return top
end

local function navCornerOK(m, i, j, k, jumpMax)
    if k <= 4 then return true end
    local e = NAV_DIRS[k]
    return Nav.edge(m, i, j, NAV_DIR_OF[e[1]][0], jumpMax) < 2
        and Nav.edge(m, i, j, NAV_DIR_OF[0][e[2]], jumpMax) < 2
end

function Nav.plan(m, sx, sz, gx, gz, jumpMax, maxExpand)
    local si, sj = Nav.cellOf(m, sx, sz)
    local gi, gj = Nav.cellOf(m, gx, gz)
    if not si or not gi then return nil, false end
    local n, C = m.n, m.C
    local start, goal = navIdx(m, si, sj), navIdx(m, gi, gj)
    local function hcost(i, j)
        local dx, dz = math.abs(i - gi), math.abs(j - gj)
        return C * (math.max(dx, dz) + (NAV_SQ2 - 1) * math.min(dx, dz))
    end
    local g, came, jumpIn, climbIn, closed = { [start] = 0 }, {}, {}, {}, {}
    local hf, hv = {}, {}
    navPush(hf, hv, hcost(si, sj), start)
    local best, bestH = start, hcost(si, sj)
    local expanded, cap = 0, maxExpand or 3000
    while #hv > 0 do
        local a = navPop(hf, hv)
        if a == goal then best = goal break end
        if not closed[a] then
            closed[a] = true
            expanded += 1
            if expanded > cap then break end
            local i, j = (a - 1) % n, (a - 1) // n
            local hh = hcost(i, j)
            if hh < bestH then best, bestH = a, hh end
            for k = 1, 8 do
                local e = NAV_DIRS[k]
                local bi, bj = i + e[1], j + e[2]
                if bi >= 0 and bj >= 0 and bi < n and bj < n then
                    local b = navIdx(m, bi, bj)
                    if not closed[b] then
                        local cls = Nav.edge(m, i, j, k, jumpMax)
                        if cls ~= 2 and navCornerOK(m, i, j, k, jumpMax) then
                            local stepLen = (k <= 4) and C or C * NAV_SQ2
                            local cost = stepLen * (1 + 0.35 * (m.near[b] or 0))
                                + (cls == 1 and 1.5 * C or 0)
                                + (cls == 3 and 20 * C or 0)
                            local ng = g[a] + cost
                            if g[b] == nil or ng < g[b] then
                                g[b], came[b] = ng, a
                                jumpIn[b], climbIn[b] = (cls == 1), (cls == 3)
                                navPush(hf, hv, ng + hcost(bi, bj), b)
                            end
                        end
                    end
                end
            end
        end
    end
    local cells, a = {}, best
    while a do
        table.insert(cells, 1, a)
        a = came[a]
    end
    local nodes = {}
    for _, c in ipairs(cells) do
        local i, j = (c - 1) % n, (c - 1) // n
        local x, z = Nav.center(m, i, j)
        table.insert(nodes, { x = x, z = z, y = m.H[c] or 0, i = i, j = j,
            jump = jumpIn[c] or false, climb = climbIn[c] or false })
    end
    return nodes, best == goal
end

local function navLineClear(m, ax, az, bx, bz, jumpMax)
    local dx, dz = bx - ax, bz - az
    local steps = math.max(1, math.ceil(math.sqrt(dx * dx + dz * dz) / (m.C * 0.5)))
    local pi, pj = Nav.cellOf(m, ax, az)
    if not pi then return false end
    for s = 1, steps do
        local t = s / steps
        local ci, cj = Nav.cellOf(m, ax + dx * t, az + dz * t)
        if not ci then return false end
        if ci ~= pi or cj ~= pj then
            local di, dj = ci - pi, cj - pj
            if math.abs(di) > 1 or math.abs(dj) > 1 then return false end
            local k = NAV_DIR_OF[di][dj]
            if Nav.edge(m, pi, pj, k, jumpMax) ~= 0 then return false end
            if k > 4 and (Nav.edge(m, pi, pj, NAV_DIR_OF[di][0], jumpMax) ~= 0
                or Nav.edge(m, pi, pj, NAV_DIR_OF[0][dj], jumpMax) ~= 0) then
                return false
            end
            if s < steps and (m.near[navIdx(m, ci, cj)] or 0) > 0 then return false end
            pi, pj = ci, cj
        end
    end
    return true
end

function Nav.smooth(m, nodes, jumpMax)
    if #nodes <= 2 then return nodes end
    local out, a = { nodes[1] }, 1
    while a < #nodes do
        local far = a + 1
        if not (nodes[a + 1].jump or nodes[a + 1].climb) then
            for c = a + 2, #nodes do
                if nodes[c].jump or nodes[c].climb then break end
                if navLineClear(m, nodes[a].x, nodes[a].z, nodes[c].x, nodes[c].z, jumpMax) then
                    far = c
                else
                    break
                end
            end
        end
        table.insert(out, nodes[far])
        a = far
    end
    return out
end

function Nav.riseTime(v0, grav, rise)
    local disc = v0 * v0 - 2 * grav * rise
    if disc < 0 then return nil end
    return (v0 - math.sqrt(disc)) / grav
end

function Nav.dirToward(dx, dz)
    local a = math.atan2(dz, dx)
    local oct = math.floor(a / (math.pi / 4) + 0.5) % 8
    local map = { [0] = { 1, 0 }, { 1, 1 }, { 0, 1 }, { -1, 1 },
                  { -1, 0 }, { -1, -1 }, { 0, -1 }, { 1, -1 } }
    local v = map[oct]
    return NAV_DIR_OF[v[1]][v[2]]
end

local NAV_RADIUS, NAV_CELL = 90, 3
local navMap, navBuilding = nil, nil
local navGoal, navGoalAt = nil, 0
local navPath, navPathGoal, navPathAt, navReached, navI = nil, nil, 0, false, 2
local navClimbing = false

local function navRays()
    local excl = {}
    for _, pl in ipairs(Players:GetPlayers()) do
        if pl.Character then table.insert(excl, pl.Character) end
    end
    local enemies = workspace:FindFirstChild("Enemies")
    if enemies then table.insert(excl, enemies) end
    if waterFloor then table.insert(excl, waterFloor) end
    local rp = RaycastParams.new()
    rp.FilterType = Enum.RaycastFilterType.Exclude
    rp.FilterDescendantsInstances = excl
    rp.RespectCanCollide = true
    local function down(x, yTop, z, len)
        local hit = workspace:Raycast(Vector3.new(x, yTop, z), Vector3.new(0, -len, 0), rp)
        return hit and hit.Position.Y or nil
    end
    local function flat(x1, y, z1, x2, z2)
        return workspace:Raycast(Vector3.new(x1, y, z1), Vector3.new(x2 - x1, 0, z2 - z1), rp) ~= nil
    end
    return down, flat
end

local function navEnsure(list, mePos)
    if not CFG.TerrainMap or navBuilding then return end
    local sx, sz, c = 0, 0, 0
    for _, e in ipairs(list) do
        local p = e.root.Position
        if (p - mePos).Magnitude < 150 then sx += p.X sz += p.Z c += 1 end
    end
    local cx, cz = mePos.X, mePos.Z
    if c > 0 then cx, cz = sx / c, sz / c end
    if navMap then
        local off = math.sqrt((navMap.cx - cx) ^ 2 + (navMap.cz - cz) ^ 2)
        local meIn = Nav.cellOf(navMap, mePos.X, mePos.Z) ~= nil
        if off < NAV_RADIUS * 0.5 and meIn then return end
    end
    local m = Nav.new(cx, cz, NAV_RADIUS, NAV_CELL)
    navBuilding = m
    local down, flat = navRays()
    local top, covered = mePos.Y + 30, 0
    for k = 0, 7 do
        local a = k * math.pi / 4
        local fy = down(mePos.X + 20 * math.cos(a), top, mePos.Z + 20 * math.sin(a), 400)
        if fy and fy > mePos.Y + 1 then covered += 1 end
    end
    if covered >= 6 then top = mePos.Y + 4 end
    m.top = top
    local myEpoch = epoch
    task.spawn(function()
        local ok = pcall(Nav.survey, m, top, down, flat, 400, function()
            task.wait()
            return (not stale(myEpoch)) and CFG.TerrainMap and navBuilding == m
        end)
        if navBuilding == m then navBuilding = nil end
        if ok and m.ready then
            navMap, navPath = m, nil
            stats.navMaps += 1
        end
    end)
end

local function navHalt() navGoal, navPath = nil, nil end

local function navUsable(goal)
    if not CFG.TerrainMap then return false end
    local m = navMap
    if not (m and m.ready) then return false end
    local _, r = parts()
    if not r then return false end
    return Nav.cellOf(m, r.Position.X, r.Position.Z) ~= nil
        and Nav.cellOf(m, goal.X, goal.Z) ~= nil
end

local function navWant(goal) navGoal, navGoalAt = goal, os.clock() end

local function navJump(h)
    local grav = workspace.Gravity
    local v0
    if h.UseJumpPower then v0 = h.JumpPower else v0 = math.sqrt(2 * grav * math.max(h.JumpHeight, 0)) end
    if v0 < 20 then v0 = 50 end
    return v0, grav, 0.85 * v0 * v0 / (2 * grav)
end

local function climbUp(topY, fx, fz)
    local _, r, h = parts()
    if not r or not h then return false end
    local myEpoch = epoch
    local v0  = math.max((navJump(h)), 50)
    local cap = math.max(2, math.floor(CFG.ClimbJumps or 8))
    local over = topY + 3 + 1.5
    local boosts = 0
    local function kick(r2, h2, keepFlat)
        boosts += 1
        stats.airJumps += 1
        lastJumpAt = os.clock()
        pcall(function() h2:ChangeState(Enum.HumanoidStateType.Freefall) end)
        local v = r2.AssemblyLinearVelocity
        r2.AssemblyLinearVelocity = keepFlat and Vector3.new(v.X, v0, v.Z)
            or Vector3.new(0, v0, 0)
    end
    h:MoveTo(r.Position)
    local t0 = os.clock()
    while os.clock() - t0 < 4 do
        if stale(myEpoch) or not P.running then return false end
        local _, r2, h2 = parts()
        if not r2 or not h2 then return false end
        if r2.Position.Y >= over then break end
        if r2.AssemblyLinearVelocity.Y < 6 then
            if boosts >= cap then break end
            kick(r2, h2, false)
        end
        task.wait()
    end
    local _, r3, h3 = parts()
    if not r3 or not h3 then return false end
    h3:MoveTo(Vector3.new(fx, topY + 3, fz))
    local t1 = os.clock()
    while os.clock() - t1 < 1.2 do
        if stale(myEpoch) or not P.running then return false end
        local _, r4, h4 = parts()
        if not r4 or not h4 then return false end
        if h4.FloorMaterial ~= Enum.Material.Air and r4.Position.Y > topY + 1.5 then
            return true
        end
        if r4.AssemblyLinearVelocity.Y < -4 and r4.Position.Y < over and boosts < cap then
            kick(r4, h4, true)
        end
        task.wait()
    end
    local _, r5 = parts()
    return r5 ~= nil and r5.Position.Y > topY + 1.5
end

local function navLearnAhead()
    local m, path = navMap, navPath
    local _, r = parts()
    if not (m and path and r) then return end
    local nd = path[math.min(navI, #path)]
    local ci, cj = Nav.cellOf(m, r.Position.X, r.Position.Z)
    if not ci then return end
    Nav.block(m, ci, cj, Nav.dirToward(nd.x - r.Position.X, nd.z - r.Position.Z))
    navPath = nil
    stats.navLearned += 1
end

local function navTick()
    if navClimbing or not navGoal then return end
    local now = os.clock()
    if now - navGoalAt > 0.5 or not P.running or not CFG.TerrainMap then
        navHalt()
        return
    end
    local m = navMap
    local _, r, h = parts()
    if not (m and m.ready and r and h) then return end
    local me, goal = r.Position, navGoal
    local v0, grav, jumpMax = navJump(h)

    local replan = navPath == nil
        or (navPathGoal and ((goal.X - navPathGoal.X) ^ 2 + (goal.Z - navPathGoal.Z) ^ 2) > 9)
        or now - navPathAt > 1.5
    if navPath and not replan then
        local nd = navPath[math.min(navI, #navPath)]
        if (nd.x - me.X) ^ 2 + (nd.z - me.Z) ^ 2 > (NAV_CELL * 6) ^ 2 then replan = true end
    end
    if replan and (navPath == nil or now - navPathAt > 0.2) then
        local nodes, reached = Nav.plan(m, me.X, me.Z, goal.X, goal.Z, jumpMax, 3000)
        navPath = nodes and Nav.smooth(m, nodes, jumpMax) or nil
        navPathGoal, navPathAt, navReached, navI = goal, now, reached, 2
        stats.navPlans += 1
    end
    local path = navPath
    if not path or #path < 2 then
        h:MoveTo(goal)
        return
    end

    while navI < #path do
        local a, b = path[navI], path[navI + 1]
        local ax, az = me.X - a.x, me.Z - a.z
        local near = ax * ax + az * az < 2.5 * 2.5
        local beyond = ax * (b.x - a.x) + az * (b.z - a.z) > 0
        local up = me.Y > a.y + 2.2
        if (near or beyond) and (not (a.jump or a.climb) or up) then
            navI += 1
        else
            break
        end
    end
    local nd = path[navI]

    if nd.climb and navI > 1 then
        local pv = path[navI - 1]
        local ex, ez = (pv.x + nd.x) / 2, (pv.z + nd.z) / 2
        local dx, dz = ex - me.X, ez - me.Z
        if dx * dx + dz * dz <= (NAV_CELL + 0.5) ^ 2 then
            navClimbing = true
            stats.navClimbs += 1
            say("air-jumping up the wall")
            local top, fx, fz = nd.y, nd.x, nd.z
            task.spawn(function()
                pcall(climbUp, top, fx, fz)
                navClimbing = false
                navPath = nil
            end)
            return
        end
    end

    local tx, tz, ty = nd.x, nd.z, nd.y
    if navI == #path then
        local dx, dz = me.X - nd.x, me.Z - nd.z
        if navReached or dx * dx + dz * dz < 4 * 4 then
            tx, tz, ty = goal.X, goal.Z, goal.Y - 3
        end
    else
        local look = math.clamp(h.WalkSpeed * 0.25, 5, 14)
        local dx, dz = nd.x - me.X, nd.z - me.Z
        local dn = math.sqrt(dx * dx + dz * dz)
        local nx = path[navI + 1]
        if dn < look and not (nd.jump or nd.climb or nx.jump or nx.climb) then
            local sx, sz = nx.x - nd.x, nx.z - nd.z
            local sl = math.sqrt(sx * sx + sz * sz)
            if sl > 0.01 then
                local t = math.min(1, (look - dn) / sl)
                tx, tz, ty = nd.x + sx * t, nd.z + sz * t, nd.y + (nx.y - nd.y) * t
            end
        end
    end
    h:MoveTo(Vector3.new(tx, ty + 3, tz))

    for k = navI, math.min(#path, navI + 1) do
        local jn = path[k]
        if jn.jump and k > 1 then
            local pv = path[k - 1]
            local ex, ez = (pv.x + jn.x) / 2, (pv.z + jn.z) / 2
            local rise = math.max(0.8, jn.y - pv.y) + 0.6
            local t = Nav.riseTime(v0, grav, rise) or 0.3
            local lead = h.WalkSpeed * t + 1.0
            local dx, dz = ex - me.X, ez - me.Z
            if dx * dx + dz * dz <= lead * lead
                and h.FloorMaterial ~= Enum.Material.Air
                and now - lastJumpAt > 0.35 then
                jump()
                lastJumpAt = now
                stats.navJumps += 1
            end
            break
        end
    end
end

P.busoOK   = false
P.kenDone  = false
local kenChar     = nil
local seenChar    = nil
local seenCharAt  = 0
local busoTries   = 0
local lastBusoAt  = 0
local kenNextAt   = 0
local kenVerifyAt = nil
local kenSeen     = false
local kenMisses   = 0
local kenBlind    = false
P.kenNote = "not checked yet"

local function hasBuso()
    local char = player.Character
    return char ~= nil and char:FindFirstChild("HasBuso") ~= nil
end
P.hasBuso = hasBuso

local function kenOn()
    local pg = player:FindFirstChildOfClass("PlayerGui")
    local sg = pg and pg:FindFirstChild("ScreenGui")
    if not sg then return nil end
    return sg:FindFirstChild("ImageLabel") ~= nil
end
P.kenOn = kenOn
P.kenNextIn = function() return math.max(0, kenNextAt - os.clock()) end

local function keepHaki()
    local char, root, hum = parts()
    if not char or not root or not hum then return end
    if char ~= seenChar then
        seenChar, seenCharAt = char, os.clock()
        busoTries = 0
    end
    if os.clock() - seenCharAt < 1.5 then return end

    if CFG.AutoBuso then
        if hasBuso() then
            P.busoOK = true
        else
            P.busoOK = false
            if busoTries < 3 and os.clock() - lastBusoAt > 2.5 then
                lastBusoAt = os.clock()
                busoTries += 1
                stats.hakiPresses += 1
                pressKey(Enum.KeyCode.J)
                say("enhancement off - pressing J")
            end
        end
    end

    if not CFG.AutoKen then return end
    local now = os.clock()
    local on  = kenOn()
    if on then kenSeen, kenBlind, kenMisses = true, false, 0 end

    if kenVerifyAt and now >= kenVerifyAt then
        kenVerifyAt = nil
        if on then
            P.kenNote = "ON - E worked, dodge counter showing"
        elseif on == false then
            kenMisses += 1
            kenNextAt = now + 20
            if not kenSeen and kenMisses >= 2 then
                kenBlind = true
                P.kenNote = "E pressed twice, dodge counter never appeared - timed check paused"
            else
                P.kenNote = "E pressed, counter not up yet - trying again in 20s"
            end
        end
    end
    if kenVerifyAt then return end

    local newLife = (kenChar ~= char)
    if not newLife and now < kenNextAt then return end

    if newLife then
        local ready
        if CFG.AutoBuso then
            ready = hasBuso()
        else
            ready = (now - seenCharAt) > 3
        end
        if not ready then return end
    end
    kenChar   = char
    kenNextAt = now + math.max(30, CFG.KenEvery or 300)
    P.kenDone = true

    if on then
        P.kenNote = "ON - checked, left alone"
        return
    end
    if on == false and kenBlind and not newLife then
        P.kenNote = "counter not showing, but the marker is unproven - not pressing"
        return
    end
    if on == nil and not newLife then
        P.kenNote = "cannot see PlayerGui.ScreenGui - timed check skipped"
        return
    end
    stats.hakiPresses += 1
    pressKey(Enum.KeyCode.E)
    say("observation off - pressing E")
    P.kenNote = "OFF - pressed E, checking"
    if on ~= nil then kenVerifyAt = now + 2.5 end
end

local SKILL_KEYS = {
    { "SkillZ", Enum.KeyCode.Z },
    { "SkillX", Enum.KeyCode.X },
    { "SkillC", Enum.KeyCode.C },
    { "SkillV", Enum.KeyCode.V },
}
local skillIndex = 0
local function activeSkills()
    local out = {}
    for _, row in ipairs(SKILL_KEYS) do
        if CFG[row[1]] then table.insert(out, row[2]) end
    end
    return out
end
P.activeSkillCount = function() return #activeSkills() end

local function swing()
    stats.swings += 1
    swingIndex += 1
    if CFG.M1 then pressM1() end
    local keys = activeSkills()
    if #keys > 0 then
        local every = math.max(1, math.floor(CFG.SkillEvery or 4))
        if (not CFG.M1) or (swingIndex % every == 0) then
            skillIndex = (skillIndex % #keys) + 1
            pressKey(keys[skillIndex])
        end
    end
end

local function swingGap() return jitter(CFG.SwingMin or 0.12, CFG.SwingMax or 0.30) end

local function swingWait(hum, targetRoot, reach)
    local deadline = os.clock() + swingGap()
    repeat
        task.wait()
        if not hum or hum.Parent == nil or hum.Health <= 0 then return end
        if targetRoot and reach then
            local _, r = parts()
            if r and (targetRoot.Position - r.Position).Magnitude > reach + 4 then
                return
            end
        end
    until os.clock() >= deadline
end
local function restGap()  return jitter(CFG.RestMin or 0, CFG.RestMax or 0) end

local DASH_KEYS = {
    Q = Enum.KeyCode.Q, E = Enum.KeyCode.E, F = Enum.KeyCode.F,
    R = Enum.KeyCode.R, LeftShift = Enum.KeyCode.LeftShift,
}
local lastDashAt = 0

local function turnCameraAt(targetPos)
    local cam = workspace.CurrentCamera
    if not cam then return false end
    local here = cam.CFrame.Position
    local flat = targetPos - here
    flat = Vector3.new(flat.X, 0, flat.Z)
    if flat.Magnitude < 0.5 then return false end
    local f    = flat.Unit
    local sinP = math.clamp(cam.CFrame.LookVector.Y, -0.99, 0.99)
    local cosP = math.sqrt(1 - sinP * sinP)
    local look = Vector3.new(f.X * cosP, sinP, f.Z * cosP)
    return pcall(function()
        cam.CFrame = CFrame.lookAt(here, here + look)
    end)
end

local function tryDash(distance, toward)
    if not CFG.Dash then return false end
    if distance and distance < (CFG.DashFrom or 25) then return false end
    if os.clock() - lastDashAt < (CFG.DashCooldown or 0.9) then return false end

    local _, r = parts()
    if not r then return false end
    local want = toward and Vector3.new(toward.X, 0, toward.Z) or nil
    if not want or want.Magnitude < 0.1 then return false end

    if CFG.DashTurnsCamera then
        if not turnCameraAt(r.Position + toward) then return false end
    else
        local cam = workspace.CurrentCamera
        if not cam then return end
        local look = cam.CFrame.LookVector
        look = Vector3.new(look.X, 0, look.Z)
        if look.Magnitude < 0.1 then return false end
        if look.Unit:Dot(want.Unit) < 0.7 then return false end
    end

    lastDashAt = os.clock()
    task.spawn(pressKey, DASH_KEYS[CFG.DashKey or "Q"] or Enum.KeyCode.Q)
    stats.dashes += 1
    return true
end

local function dashDir(r, dir)
    turnCameraAt(r.Position + dir * 20)
    task.wait()
    pressKey(DASH_KEYS[CFG.DashKey or "Q"] or Enum.KeyCode.Q)
    lastDashAt = os.clock()
    stats.dashes += 1
    stats.panicDashes += 1
end

local function panicGuard(myEpoch)
    return stale(myEpoch) or not P.running or not moveEnabled
end

local function climbBurst(targetRoot)
    navHalt()
    local _, r, h = parts()
    if not r or not h or not targetRoot then return false end
    local start = r.Position
    local flat  = targetRoot.Position - start
    flat = Vector3.new(flat.X, 0, flat.Z)
    if flat.Magnitude < 0.5 then return false end
    local goal = targetRoot.Position
    local ok = climbUp(goal.Y - 3, goal.X, goal.Z)
    stats.hops += 1
    local _, r4 = parts()
    if not r4 then return false end
    return ok or (r4.Position - start):Dot(flat.Unit) > 4
end

local function lateralBurst(targetRoot, side)
    navHalt()
    local _, r, h = parts()
    if not r or not h or not targetRoot then return false end
    local start = r.Position
    local flat  = targetRoot.Position - start
    flat = Vector3.new(flat.X, 0, flat.Z)
    if flat.Magnitude < 0.5 then return false end
    local dir = flat.Unit
    local lat = Vector3.new(-dir.Z * side, 0, dir.X * side)
    local myEpoch = epoch

    h:MoveTo(r.Position)
    task.wait(0.12)
    for _ = 1, 2 do
        if panicGuard(myEpoch) then return false end
        local _, r2, h2 = parts()
        if not r2 or not h2 then return false end
        h2:MoveTo(r2.Position)
        dashDir(r2, lat)
        task.wait(0.55)
    end

    local _, r3, h3 = parts()
    if not r3 or not h3 then return false end
    local goal = targetRoot.Position
    h3:MoveTo(Vector3.new(goal.X, r3.Position.Y, goal.Z))
    task.wait(0.6)
    local _, r4 = parts()
    if not r4 then return false end
    local moved = r4.Position - start
    local flatMoved = Vector3.new(moved.X, 0, moved.Z).Magnitude
    local ok = moved:Dot(dir) > 4 or flatMoved > 12
    if ok then lastSide = side end
    return ok
end
P.tryDash = tryDash

local function cancelWalk()
    local _, r, h = parts()
    if r and h then h:MoveTo(r.Position) end
end

local function faceTarget(root, targetPos, tight)
    local flat = Vector3.new(targetPos.X, root.Position.Y, targetPos.Z)
    if (flat - root.Position).Magnitude < 0.5 then return end
    local want = CFrame.new(root.Position, flat)
    local slop = tight and 0.9995 or 0.94
    if root.CFrame.LookVector:Dot(want.LookVector) > slop then return end
    root.CFrame = want
end

local camHeld = false
local function releaseCamera()
    if not camHeld then return end
    camHeld = false
    local cam = workspace.CurrentCamera
    if not cam then return end
    pcall(function()
        local _, _, hum = parts()
        if hum then cam.CameraSubject = hum end
        cam.CameraType = Enum.CameraType.Custom
    end)
end
P.releaseCamera = releaseCamera

local lastCamAt = 0
local function aimCameraAt(root, targetPos)
    if not CFG.AimCamera then return end
    local cam = workspace.CurrentCamera
    if not cam or not root then return end
    if os.clock() - lastCamAt < 0.06 then return end
    lastCamAt = os.clock()

    local eye  = root.Position + Vector3.new(0, 2, 0)
    local flat = targetPos - eye
    flat = Vector3.new(flat.X, 0, flat.Z)
    if flat.Magnitude < 0.5 then return end
    local back = eye - flat.Unit * (CFG.CamBack or 13)
        + Vector3.new(0, CFG.CamUp or 5, 0)

    pcall(function()
        if not camHeld then
            cam.CameraType = Enum.CameraType.Scriptable
            camHeld = true
        end
        cam.CFrame = CFrame.new(back, targetPos)
        local vs = cam.ViewportSize
        VIM:SendMouseMoveEvent(vs.X * 0.5, vs.Y * 0.5, game)
    end)
end

local function walkTo(goal, opts)
    navHalt()
    opts = opts or {}
    local _, root, hum = parts()
    if not root or not hum then return false end
    local arrive = opts.arrive or 6
    local budget = opts.budget or 30
    if (root.Position - goal).Magnitude <= arrive then return true end
    stats.walks += 1

    local path = PathService:CreatePath({
        AgentRadius     = 3,
        AgentHeight     = 6,
        AgentCanJump    = true,
        AgentMaxSlope   = 60,
        WaypointSpacing = 8,
    })

    local myEpoch = epoch
    local deadline, retries = os.clock() + budget, 0
    while os.clock() < deadline and moveEnabled and not stale(myEpoch) do
        local _, r, h = parts()
        if not r or not h then return false end
        if (r.Position - goal).Magnitude <= arrive then return true end
        local ok = pcall(function() path:ComputeAsync(r.Position, goal) end)
        local points = (ok and path.Status == Enum.PathStatus.Success)
            and path:GetWaypoints() or nil

        if not points or #points < 2 then
            local before = r.Position
            h:MoveTo(goal)
            task.wait(1.0)
            local _, r2 = parts()
            if not r2 then return false end
            if (r2.Position - before).Magnitude < 1.5 then
                if CFG.JumpWhenStuck then h.Jump = true end
                retries += 1
                if retries > 5 then return false end
            end
        else
            for i = 2, #points do
                if not moveEnabled or stale(myEpoch) then return false end
                local wp = points[i]
                local _, r3, h3 = parts()
                if not r3 or not h3 then return false end

                if wp.Action == Enum.PathWaypointAction.Jump then h3.Jump = true end
                h3:MoveTo(wp.Position)

                local reached, stamp = false, r3.Position
                local wpDeadline = os.clock() + 3
                local lastWp = (i == #points)
                while os.clock() < wpDeadline do
                    if stale(myEpoch) then return false end
                    local _, r4, h4 = parts()
                    if not r4 or not h4 then return false end
                    if (r4.Position - goal).Magnitude <= arrive then return true end
                    local off  = wp.Position - r4.Position
                    local lead = lastWp and 4 or math.clamp(h4.WalkSpeed * 0.1, 4, 8)
                    if Vector3.new(off.X, 0, off.Z).Magnitude < lead and math.abs(off.Y) < 6 then
                        reached = true
                        break
                    end
                    task.wait()
                end

                if not reached then
                    local _, r5, h5 = parts()
                    if r5 and (r5.Position - stamp).Magnitude < 1.5 then
                        if CFG.JumpWhenStuck and h5 then h5.Jump = true end
                        retries += 1
                        if retries > 5 then return false end
                        break
                    end
                end
                if os.clock() > deadline then break end
            end
        end
    end

    local _, rf = parts()
    return rf ~= nil and (rf.Position - goal).Magnitude <= arrive + 8
end
P.walkTo = walkTo

local function station(targetRoot, climb)
    local _, r, h = parts()
    if not r or not h or not targetRoot then return math.huge end

    local me, them = r.Position, targetRoot.Position
    local flat = Vector3.new(them.X - me.X, 0, them.Z - me.Z)
    local d = flat.Magnitude
    if d < 0.05 then return d end
    local dir = flat.Unit

    local want  = math.max(CFG.StandOff or 8, 1)
    local slack = math.max(CFG.StandSlack or 2, 0.5)
    local spot  = them - dir * want

    if d > want + slack or climb then
        if os.clock() < pathUntil then
            walkTo(them, { arrive = want + slack, budget = 1.5 })
        elseif navUsable(climb and them or spot) then
            navWant(climb and them or spot)
        elseif d > 120 then
            walkTo(spot, { arrive = want + slack, budget = 4 })
        else
            navHalt()
            local goal = climb and them or spot
            h:MoveTo(Vector3.new(goal.X, me.Y, goal.Z))
        end
    elseif d < want - slack then
        navHalt()
        h:MoveTo(Vector3.new(spot.X, me.Y, spot.Z))
        if CFG.FaceLock then faceTarget(r, them, true) end
    else
        navHalt()
        h:MoveTo(me)
        faceTarget(r, them, CFG.FaceLock)
    end
    return d
end

local nameCache = {}
local function cleanName(model)
    local hit = nameCache[model]
    if hit then return hit end
    local n = (model.Name:gsub("%s*%b[]", ""):gsub("^%s+", ""):gsub("%s+$", ""))
    nameCache[model] = n
    return n
end

local function isBlacklisted(model)
    local until_ = blacklist[model]
    if not until_ then return false end
    if os.clock() > until_ then blacklist[model] = nil return false end
    return true
end

local function liveEnemies(name)
    local folder = workspace:FindFirstChild("Enemies")
    if not folder then return {} end
    local out = {}
    for _, m in ipairs(folder:GetChildren()) do
        if m:IsA("Model") and not isBlacklisted(m) then
            local hum  = m:FindFirstChildOfClass("Humanoid")
            local root = m:FindFirstChild("HumanoidRootPart")
            if hum and root and hum.Health > 0 then
                local n = cleanName(m)
                if (not name) or n == name then
                    table.insert(out, { model = m, hum = hum, root = root, name = n })
                end
            end
        end
    end
    return out
end
P.liveEnemies = liveEnemies

local function swingReach()
    return math.max(CFG.StandOff or 8, 1) + math.max(CFG.StandSlack or 2, 0.5) * 2
end

local SWITCH_MARGIN = 6

local function pickNext(list, pos)
    local best, bestD = nil, math.huge
    local reach = swingReach()
    for _, e in ipairs(list) do
        local d = (e.root.Position - pos).Magnitude
        if e.model == engagedModel and d <= reach then return e, d end
        if d < bestD then best, bestD = e, d end
    end
    return best, bestD
end

function P.nearbyNames()
    local folder = workspace:FindFirstChild("Enemies")
    local counts = {}
    if folder then
        for _, m in ipairs(folder:GetChildren()) do
            if m:IsA("Model") then
                local hum = m:FindFirstChildOfClass("Humanoid")
                if hum and hum.Health > 0 then
                    local n = cleanName(m)
                    counts[n] = (counts[n] or 0) + 1
                end
            end
        end
    end
    return counts
end

local function levelRow()
    local lv = playerLevel()
    if not lv then return nil end
    for _, row in ipairs(LEVELS) do
        if lv >= row[1] and lv <= row[2] then return row end
    end
    return LEVELS[#LEVELS]
end
P.levelRow = levelRow

local function resolveTarget()
    if CFG.Target and #tostring(CFG.Target) > 0 then
        local name = CFG.Target
        local spot
        for _, row in ipairs(LEVELS) do
            if row[3] == name then spot = row[4] break end
        end
        return name, spot
    end
    local row = levelRow()
    if not row then return nil, nil end
    return row[3], row[4]
end

local remotes = RS:FindFirstChild("Remotes")
local commF   = remotes and remotes:FindFirstChild("CommF_")

local function npcSources()
    local out = {}
    for _, n in ipairs({ "NPCs", "Npcs", "Characters", "Map" }) do
        local f = workspace:FindFirstChild(n)
        if f then table.insert(out, f) end
    end
    table.insert(out, workspace)
    return out
end

local function anchorPart(model)
    return model.PrimaryPart
        or model:FindFirstChild("HumanoidRootPart")
        or model:FindFirstChild("Head")
        or model:FindFirstChild("Torso")
        or model:FindFirstChildWhichIsA("BasePart")
end

local function questMarker(model)
    local ok, hit = pcall(function()
        for _, d in ipairs(model:GetDescendants()) do
            if d:IsA("BillboardGui") then
                for _, t in ipairs(d:GetDescendants()) do
                    if (t:IsA("TextLabel") or t:IsA("TextButton"))
                        and type(t.Text) == "string"
                        and string.find(string.lower(t.Text), "quest", 1, true) then
                        return true
                    end
                end
            end
        end
        return false
    end)
    return ok and hit or false
end

local function findQuestGiver(maxRange, wantName, markerOnly)
    local _, root = parts()
    if not root then return nil end
    maxRange = maxRange or 300
    local want = wantName and string.lower(wantName) or nil

    local cands, seen = {}, {}
    for _, src in ipairs(npcSources()) do
        for _, m in ipairs(src:GetChildren()) do
            if m:IsA("Model") and not seen[m] then
                seen[m] = true
                local part = anchorPart(m)
                if part then
                    local d = (part.Position - root.Position).Magnitude
                    if d <= maxRange then
                        local low   = string.lower(m.Name)
                        local named = string.find(low, "quest", 1, true)
                                   or string.find(low, "giver", 1, true)
                        local known  = KNOWN_GIVERS[low] ~= nil
                        local marker = questMarker(m)
                        local exact  = want and (low == want)
                        local score = d
                            - (exact and 50000 or 0)
                            - (known and 20000 or 0)
                            - (marker and 5000 or 0)
                            - (named and 1000 or 0)
                        local accept = exact or known or marker or named
                            or m:FindFirstChildOfClass("Humanoid")
                        if markerOnly then
                            accept = (exact or known or marker) and true or false
                        end
                        if accept then
                            table.insert(cands, {
                                model = m, part = part, dist = d, name = m.Name,
                                score = score,
                                signal = (exact and "exact name")
                                      or (known and "known giver")
                                      or (marker and "QUEST marker")
                                      or (named and "name") or "npc",
                            })
                        end
                    end
                end
            end
        end
    end

    table.sort(cands, function(a, b) return a.score < b.score end)
    P.questCandidates = cands
    local best = cands[1]
    return best, best and best.dist or nil
end
P.findQuestGiver = findQuestGiver

function P.questScan(range)
    findQuestGiver(range or 400)
    local out = {}
    for i, c in ipairs(P.questCandidates or {}) do
        if i > 8 then break end
        table.insert(out, string.format("%s  %.0f studs  (%s)",
            tostring(c.name), c.dist, c.signal))
    end
    if #out == 0 then return { "no NPC models in range" } end
    return out
end

local function shownOnScreen(g)
    local o = g
    while o and o:IsA("GuiObject") do
        if not o.Visible then return false end
        o = o.Parent
    end
    return true
end

local function blockText(frame)
    local acc = {}
    for _, d in ipairs(frame:GetDescendants()) do
        if (d:IsA("TextLabel") or d:IsA("TextButton")) and type(d.Text) == "string" then
            table.insert(acc, d.Text)
        end
    end
    return string.lower(table.concat(acc, " "))
end

local questCache, questCacheAt = nil, 0
local questLabel = nil
P.questScans = 0

local function parseCounter(d)
    if not d or not d.Parent then return nil end
    local txt = d.Text
    if type(txt) ~= "string" or #txt == 0 then return nil end
    local have, need = string.match(txt, "(%d+)%s*/%s*(%d+)")
    if not (have and need) then return nil end
    if not shownOnScreen(d) then return nil end
    local blob = d.Parent and blockText(d.Parent) or string.lower(txt)
    if not (string.find(blob, "defeat", 1, true)
        or string.find(blob, "eliminate", 1, true)
        or string.find(blob, "kill", 1, true)) then return nil end
    local enemy = string.match(blob, "defeat%s+%d+%s+([%a%s\'%-]+)")
    if enemy then enemy = (enemy:gsub("%s+$", "")) end
    return {
        have = tonumber(have) or 0, need = tonumber(need) or 0,
        enemy = enemy, text = txt,
    }
end

function P.readQuest(force)
    if not force and (os.clock() - questCacheAt) < 0.5 then return questCache end
    questCacheAt = os.clock()

    local fast
    pcall(function() fast = parseCounter(questLabel) end)
    if fast then
        questCache = (fast.need > 0) and fast or nil
        return questCache
    end
    questLabel = nil

    local pg = player:FindFirstChild("PlayerGui")
    if not pg then questCache = nil return nil end
    local found
    P.questScans += 1
    pcall(function()
        for _, d in ipairs(pg:GetDescendants()) do
            if d:IsA("TextLabel") and not d:FindFirstAncestor("BFPHUD") then
                local parsed = parseCounter(d)
                if parsed then
                    questLabel = d
                    found = parsed
                    return
                end
            end
        end
    end)
    questCache = (found and found.need > 0) and found or nil
    return questCache
end

function P.questActive() return P.readQuest() ~= nil end

local function clickQuestDialog(wantName)
    local pg = player:FindFirstChild("PlayerGui")
    if not pg then return false end

    local function textOf(b)
        local acc = {}
        if type(b.Text) == "string" and #b.Text > 0 then table.insert(acc, b.Text) end
        for _, d in ipairs(b:GetDescendants()) do
            if (d:IsA("TextLabel") or d:IsA("TextBox"))
                and type(d.Text) == "string" and #d.Text > 0 then
                table.insert(acc, d.Text)
            end
        end
        return string.lower(table.concat(acc, " "))
    end

    local function click(b)
        local fired = false
        pcall(function()
            if getconnections then
                for _, conn in ipairs(getconnections(b.Activated)) do
                    conn:Fire() fired = true
                end
                if not fired then
                    for _, conn in ipairs(getconnections(b.MouseButton1Click)) do
                        conn:Fire() fired = true
                    end
                end
            end
        end)
        if not fired then
            pcall(function()
                local ap, as = b.AbsolutePosition, b.AbsoluteSize
                local x, y = ap.X + as.X / 2, ap.Y + as.Y / 2
                VIM:SendMouseButtonEvent(x, y, 0, true, game, 0)
                task.wait(0.06)
                VIM:SendMouseButtonEvent(x, y, 0, false, game, 0)
            end)
        end
    end

    local deadline = os.clock() + 4
    while os.clock() < deadline do
        local best, fallback, seen = nil, nil, {}
        for _, d in ipairs(pg:GetDescendants()) do
            local mine = d:FindFirstAncestor("BFPHUD") ~= nil
            if not mine and d:IsA("GuiButton") and d.Visible and d.AbsoluteSize.X > 20 then
                local txt = textOf(d)
                if #txt > 2 then
                    table.insert(seen, string.sub(txt, 1, 40))
                    if wantName and string.find(txt, string.lower(wantName), 1, true) then
                        best = d
                    elseif string.find(txt, "quest", 1, true)
                        or string.find(txt, "accept", 1, true)
                        or string.find(txt, "kill", 1, true)
                        or string.find(txt, "defeat", 1, true) then
                        fallback = fallback or d
                    end
                end
            end
        end
        P.lastQuestOptions = seen
        local pick = best or fallback
        if pick then
            click(pick)
            return true, string.sub(textOf(pick), 1, 60)
        end
        task.wait(0.25)
    end
    return false
end

function P.giverFor(enemy)
    enemy = enemy or activeName or CFG.Target
    if not enemy then return nil, nil end
    local name = (CFG.QuestGiverName and #CFG.QuestGiverName > 0 and CFG.QuestGiverName)
        or P.learnedGivers[enemy] or GIVER_NAMES[enemy]
    local pos = P.giverSpots[enemy] or GIVER_POS[enemy]
    return name, pos
end

function P.setGiver(pos, name)
    local e = activeName or CFG.Target
    if not e then say("pick a target first") return false end
    P.giverSpots[e] = pos
    if name then P.learnedGivers[e] = name end
    say("giver set for " .. e .. (name and (": " .. name) or ""))
    return true
end

function P.setGiverHere()
    local _, root = parts()
    if not root then return false end
    return P.setGiver(root.Position, nil)
end

function P.clearGiver()
    local e = activeName or CFG.Target
    if e then
        P.giverSpots[e] = nil
        P.learnedGivers[e] = nil
    end
    say("giver reset to the table")
end

local questTakenAt, questBaseKills, questLastHave, questMovedAt = 0, 0, 0, 0
local questBlind, lastQuestAt = false, 0

function P.questForTarget()
    local enemy = activeName or CFG.Target
    if not enemy then return nil, nil, nil end
    if CFG.QuestName and #tostring(CFG.QuestName) > 0 then
        return CFG.QuestName, CFG.QuestTier or 1, enemy
    end
    local learned = P.learnedQuests[enemy]
    if learned then return learned.name, learned.tier, enemy end
    local q = QUESTS[enemy]
    if q then return q[1], q[2], enemy end
    return nil, nil, enemy
end
P.questForTarget = questForTarget

function P.acceptQuest(opts)
    opts = opts or {}
    if not commF then
        P.lastQuestResult = "no CommF_ remote"
        say(P.lastQuestResult)
        return false
    end
    if P.readQuest(true) and not opts.force then
        P.lastQuestResult = "already on a quest - not re-taking"
        say(P.lastQuestResult)
        return false
    end

    local qname, tier, enemy = questForTarget()
    local locked = P.lockedQuest
    if locked and not (CFG.QuestName and #tostring(CFG.QuestName) > 0) then
        qname, tier, enemy = locked.name, locked.tier, locked.enemy
    end
    if CFG.QuestTier then tier = CFG.QuestTier end
    tier = tier or 1
    if not qname then
        P.lastQuestResult = "no quest id known for " .. tostring(enemy or "this enemy")
        say(P.lastQuestResult)
        return false
    end

    local myEpoch = epoch
    local _, root = parts()
    local home = root and root.Position
    local atGiver = false

    local mode = CFG.GiverMode or "auto"

    local function goToGiver()
        local wantName, dest = P.giverFor(enemy)
        if not dest then
            local far = CFG.QuestGiverRange or 1200
            local giver
            if wantName then
                giver = findQuestGiver(500, wantName) or findQuestGiver(far, wantName)
            end
            giver = giver or findQuestGiver(500, nil, true) or findQuestGiver(far, nil, true)
            if giver then
                dest = giver.part.Position
                P.giverName = giver.name
            end
        end
        if not dest then return true end
        atGiver = true
        setState("TO GIVER")
        say("walking to the quest giver")
        walkTo(dest, { arrive = 8, budget = 60 })
        if stale(myEpoch) then return false end
        local _, r = parts()
        if r then faceTarget(r, dest) end
        task.wait(jitter(0.4, 1.0))
        return true
    end

    local _, gpos = P.giverFor(enemy)
    local giverDist = (gpos and root) and (gpos - root.Position).Magnitude or nil
    local mustWalk = (mode == "always")
        or (mode == "auto" and (giverDist == nil
            or giverDist <= (CFG.GiverWalkRadius or 250)))

    if mustWalk and not goToGiver() then
        P.lastQuestResult = "stopped on the way to the giver"
        say(P.lastQuestResult)
        return false
    end

    if stale(myEpoch) then
        P.lastQuestResult = "stopped before asking - no quest taken"
        say(P.lastQuestResult)
        return false
    end

    local mine = enemy and string.lower(tostring(enemy)) or nil
    local function wanted(trackerEnemy)
        if not trackerEnemy or not mine then return true end
        local a = string.lower(tostring(trackerEnemy))
        return string.find(a, mine, 1, true) ~= nil
            or string.find(mine, a, 1, true) ~= nil
    end

    local tiers
    if CFG.QuestTier then
        tiers = { CFG.QuestTier }
    elseif locked then
        tiers = { tier }
    else
        tiers = { tier }
        for _, t in ipairs({ 1, 2, 3 }) do
            if t ~= tier then table.insert(tiers, t) end
        end
    end

    local q, ok, res
    local function attempt()
        local gotQ, gotOk, gotRes
        for i, t in ipairs(tiers) do
            if stale(myEpoch) then break end
            gotOk, gotRes = pcall(function()
                return commF:InvokeServer("StartQuest", qname, t)
            end)
            task.wait(0.45)
            gotQ = P.readQuest(true)

            if not gotQ and atGiver and i == 1 then
                say("remote refused - talking to the NPC")
                for _ = 1, 3 do
                    pcall(function()
                        VIM:SendKeyEvent(true, Enum.KeyCode.E, false, game)
                        task.wait(0.07)
                        VIM:SendKeyEvent(false, Enum.KeyCode.E, false, game)
                    end)
                    task.wait(0.3)
                end
                pcall(clickQuestDialog, enemy)
                task.wait(0.5)
                gotQ = P.readQuest(true)
            end

            tier = t
            if not gotQ then break end
            if wanted(gotQ.enemy) then break end
            if i == #tiers then break end
        end
        return gotQ, gotOk, gotRes
    end

    q, ok, res = attempt()

    if not q and mode == "auto" and not atGiver and not stale(myEpoch) then
        say("nothing from here - walking up and asking again")
        local moved = goToGiver() and atGiver
        if moved then q, ok, res = attempt() end
    end

    local matched = (q ~= nil) and wanted(q.enemy)
    P.questMatched = matched
    questTakenAt   = os.clock()
    questBaseKills = stats.kills
    questLastHave  = q and q.have or 0
    questMovedAt   = os.clock()

    if q and enemy and matched then
        stats.quests += 1
        if P.giverName then P.learnedGivers[enemy] = P.giverName end
        local _, r = parts()
        if atGiver and r then P.giverSpots[enemy] = P.giverSpots[enemy] or r.Position end
        P.lockedQuest = { name = qname, tier = tier, enemy = enemy }
        P.learnedQuests[enemy] = { name = qname, tier = tier }
    end
    questBlind = (q == nil) and ok or false
    P.quest = q
    P.lastQuestResult = string.format("%s t%d -> %s", tostring(qname), tier,
        q and string.format("%s  %d/%d", matched and "ACTIVE" or "WRONG", q.have, q.need)
          or ("sent, tracker unreadable"))
    say(P.lastQuestResult)

    if atGiver and CFG.QuestReturnToFarm and home and not stale(myEpoch) then
        setState("TO FARM")
        say("walking back to the farm")
        walkTo(home, { arrive = 12, budget = 60 })
    end
    if P.running then
        setState("FIGHT")
        progress()
    end
    return q ~= nil or questBlind
end

function P.takeQuest() return P.acceptQuest({ force = true }) end

function P.armQuest()
    lastQuestAt   = 0
    questBlind    = false
    P.lockedQuest = nil
end

function P.questCycle()
    local q = P.readQuest(true)
    P.quest = q

    if q then
        questBlind = false
        P.questProgress = q.have .. "/" .. q.need
        if q.have ~= questLastHave then
            questLastHave, questMovedAt = q.have, os.clock()
        end
        if q.have < q.need then
            if os.clock() - questMovedAt > (CFG.QuestStallSeconds or 240) then
                say("quest has not moved - taking fresh one")
            else
                return
            end
        elseif os.clock() - questTakenAt < 2 then
            return
        else
            say("quest done - returning for next")
        end
    elseif questBlind then
        local done = stats.kills - questBaseKills
        P.questProgress = done .. "/" .. CFG.QuestKillsFallback .. " (local)"
        if done < CFG.QuestKillsFallback and os.clock() - questTakenAt < 900 then
            return
        end
    else
        P.questProgress = "none"
    end

    if os.clock() - lastQuestAt < CFG.QuestRetrySeconds then return end
    lastQuestAt = os.clock()
    P.acceptQuest({ force = (q ~= nil) })
end

local function escalate(target)
    navHalt()
    escalation = math.min(escalation + 1, 4)
    stats.escalations += 1
    lastProgressAt = os.clock()

    if escalation == 1 then
        say("stuck: re-seating")
        cancelWalk()
    elseif escalation == 2 then
        say("stuck: backing off")
        local _, r, h = parts()
        if r and h then
            h:MoveTo(r.Position - r.CFrame.LookVector * 14)
            task.wait(0.9)
        end
    elseif escalation == 3 then
        say("stuck: re-equipping weapon")
        keepWeapon()
        local _, _, h = parts()
        if h and CFG.JumpWhenStuck then h.Jump = true end
    elseif escalation == 4 then
        say("stuck: blacklisting target")
        if target then blacklist[target.model] = os.clock() + 60 end
        setState("RESOLVE")
    end
end

local function retreat()
    navHalt()
    stats.retreats += 1
    say("retreating - low health")
    setState("RETREAT")
    releaseCamera()
    local deadline = os.clock() + math.max(CFG.RegenWait, 4)
    while P.running and os.clock() < deadline do
        local _, r, h = parts()
        if not r or not h then break end
        if healthPct() > 0.9 then break end
        local away = r.Position
        local near = liveEnemies(nil)
        if #near > 0 then
            local sum = Vector3.zero
            for _, e in ipairs(near) do sum += e.root.Position end
            local threat = sum / #near
            local dir = r.Position - threat
            dir = Vector3.new(dir.X, 0, dir.Z)
            if dir.Magnitude > 0.1 then away = r.Position + dir.Unit * 70 end
        end
        h:MoveTo(away)
        task.wait(0.5)
    end
    progress()
end

local lastGatherAt = 0
local function gatherWorth(list, pos)
    if not CFG.Gather then return false end
    if os.clock() - lastGatherAt < (CFG.GatherCooldown or 6) then return false end
    local reach  = swingReach()
    local radius = CFG.GatherRadius or 60
    local inRange = 0
    for _, e in ipairs(list) do
        local d = (e.root.Position - pos).Magnitude
        if d <= reach * 1.5 then return false end
        if d <= radius then inRange += 1 end
    end
    return inRange >= 2
end

local function gatherPass(list)
    local _, r = parts()
    if not r or not gatherWorth(list, r.Position) then return end
    lastGatherAt = os.clock()

    local radius = CFG.GatherRadius or 60
    local pool = {}
    for _, e in ipairs(list) do
        if (e.root.Position - r.Position).Magnitude <= radius then
            table.insert(pool, e)
        end
    end
    local want  = math.max(2, math.floor(CFG.GatherCount or 3))
    local route, from = {}, r.Position
    while #route < want and #pool > 0 do
        local bi, bd = 1, math.huge
        for i, e in ipairs(pool) do
            local d = (e.root.Position - from).Magnitude
            if d < bd then bi, bd = i, d end
        end
        local e = table.remove(pool, bi)
        table.insert(route, e)
        from = e.root.Position
    end

    stats.gathers += 1
    setState("GATHER")
    say(string.format("gathering %d", #route))
    local reach   = swingReach()
    local myEpoch = epoch
    for _, e in ipairs(route) do
        local deadline = os.clock() + 3
        while os.clock() < deadline do
            if stale(myEpoch) or not P.running or not moveEnabled then return end
            if healthPct() < CFG.MinHealthPercent then return end
            if not e.model.Parent or e.hum.Health <= 0 then break end
            setChase(e.root.Position)
            local d = station(e.root)
            if d <= reach then
                if CFG.M1 then pressM1() end
                stats.swings += 1
                stats.tagged += 1
                progress()
                task.wait(0.12)
                break
            end
            task.wait(0.06)
        end
    end
end

local function step()
    local _, root = parts()
    if not root then
        say("waiting for character")
        task.wait(0.5)
        return
    end

    if healthPct() < CFG.MinHealthPercent then
        retreat()
        return
    end

    if state == "RESOLVE" or not activeName then
        local name, spot = resolveTarget()
        if not name then
            say("level unknown - pick a target on panel")
            task.wait(1.5)
            return
        end
        activeName, farmSpot = name, spot
        engagedModel = nil
        pathUntil = 0
        say("target: " .. name)
        setState("FIGHT")
        progress()
        return
    end

    keepWeapon()
    pcall(keepHaki)

    if CFG.QuestLoop then pcall(P.questCycle) end

    local list = liveEnemies(activeName)

    if #list == 0 then
        releaseCamera()
        if farmSpot then
            local far = (farmSpot - root.Position).Magnitude
            if far < 140 then
                say(string.format("waiting for %s", activeName))
                setState("WAIT")
                local myEpoch = epoch
                local untilT  = os.clock() + jitter(1.5, 3.5)
                while os.clock() < untilT and P.running and not stale(myEpoch) do
                    task.wait(0.1)
                    if #liveEnemies(activeName) > 0 then break end
                end
                return
            end
            if far > (CFG.MaxWalk or 1200) then
                say("target too far")
                setState("WAIT")
                task.wait(3)
                return
            end
            setState("WALK")
            walkTo(farmSpot, { arrive = 20, budget = 90 })
        else
            say("location unknown")
            task.wait(3)
        end
        return
    end

    setState("FIGHT")

    if CFG.TerrainMap then pcall(navEnsure, list, root.Position) end

    if CFG.Gather then
        pcall(gatherPass, list)
        list = liveEnemies(activeName)
        if #list == 0 then return end
        setState("FIGHT")
    end

    local want     = math.max(CFG.StandOff or 8, 1)
    local slack    = math.max(CFG.StandSlack or 2, 0.5)
    local sweepEnd = os.clock() + (CFG.SweepSeconds or 10)

    local target, bestD = pickNext(list, root.Position)
    if not target then task.wait(0.3) return end
    if engagedModel ~= target.model then pathUntil = 0 end
    engagedModel = target.model
    local lastHitAt   = os.clock()
    local targetSince = os.clock()
    local lastHP      = target.hum.Health
    local lastLookAt  = 0
    local stuckSince  = nil
    local panicked    = false
    local targetPanics = 0
    local lateralSide = nil
    local windowAt    = nil
    local windowPos   = nil
    local creeping    = false
    local targetDetours = 0
    local unreachable = false
    local targetGhosts = 0
    local targetLearn = 0

    while P.running and os.clock() < sweepEnd do
        local m    = target.model
        local hum  = target.hum
        local gone = (not m) or (not m.Parent) or (not hum) or (hum.Parent == nil)
        local dead = (not gone) and hum.Health <= 0

        if dead and not countedDead[m] then
            countedDead[m] = os.clock()
            stats.kills += 1
            progress()
            if CFG.QuestLoop and P.quest and (P.quest.need or 0) > 0
                and (stats.kills - questBaseKills) >= P.quest.need then
                local qq = P.readQuest(true)
                if (not qq) or qq.have >= qq.need then
                    break
                end
            end
        end

        local giveUp = CFG.GiveUpSeconds or 12
        local expired = (not gone) and (not dead)
            and (unreachable
                 or (os.clock() - lastHitAt) > giveUp
                 or (os.clock() - targetSince) > giveUp * 5)
        if expired then
            blacklist[m] = os.clock() + 30
        end

        if gone or dead or expired then
            if (CFG.RestMax or 0) > 0 then task.wait(restGap()) end
            local _, rNow = parts()
            if not rNow then break end
            list = liveEnemies(activeName)
            local nxt, nd = pickNext(list, rNow.Position)
            if not nxt then break end
            if gatherWorth(list, rNow.Position) then break end
            target  = nxt
            engagedModel = target.model
            lastHitAt   = os.clock()
            targetSince = os.clock()
            lastHP      = target.hum.Health
            lastLookAt  = os.clock()
            stuckSince, panicked, targetPanics, lateralSide = nil, false, 0, nil
            windowAt, windowPos, creeping = nil, nil, false
            targetDetours, unreachable, pathUntil, targetGhosts = 0, false, 0, 0
            targetLearn = 0
            task.wait()
            continue
        end

        local _, r, h = parts()
        if not r or not h then break end

        local dy    = math.abs(target.root.Position.Y - r.Position.Y)
        local climb = dy > 6
        setChase(target.root.Position)
        local d = station(target.root, climb)
        aimCameraAt(r, target.root.Position)

        local reach     = want + slack * 2
        local swingFrom = math.max(reach, CFG.SwingFrom or 0)
        local inReach   = d <= reach and not climb
        local closing   = (not inReach) and d <= swingFrom

        if inReach then
            swing()
            swingWait(hum, target.root, swingFrom)
        else
            if os.clock() - lastLookAt > 0.25 then
                lastLookAt = os.clock()
                list = liveEnemies(activeName)
                local nxt, nd = pickNext(list, r.Position)
                if nxt and nxt.model ~= target.model then
                    local cur = (target.root.Position - r.Position).Magnitude
                    if nd + SWITCH_MARGIN < cur then
                        target = nxt
                        engagedModel = target.model
                        lastHitAt   = os.clock()
                        targetSince = os.clock()
                        lastHP      = target.hum.Health
                        stuckSince, panicked, targetPanics, lateralSide = nil, false, 0, nil
                        windowAt, windowPos, creeping = nil, nil, false
                        targetDetours, unreachable, pathUntil, targetGhosts = 0, false, 0, 0
                        targetLearn = 0
                        stats.switches += 1
                        task.wait()
                        continue
                    end
                end
            end

            local now   = os.clock()
            local flatT = target.root.Position - r.Position
            flatT = Vector3.new(flatT.X, 0, flatT.Z)
            local dirT  = (flatT.Magnitude > 0.5) and flatT.Unit or nil

            local ledge = CFG.JumpWhenStuck and now - lastJumpAt > 0.9 and ledgeAhead(r, h)
            if ledge and not climb then
                jump()
                lastJumpAt = now
                stats.hops += 1
            end

            local pushing = h.MoveDirection.Magnitude > 0.1
            local vel     = r.AssemblyLinearVelocity
            local ground  = Vector3.new(vel.X, 0, vel.Z).Magnitude
            if not pushing then
                windowAt, windowPos, creeping = nil, nil, false
            else
                if not windowAt then windowAt, windowPos = now, r.Position end
                if now - windowAt >= 1.2 then
                    local moved = r.Position - windowPos
                    creeping = Vector3.new(moved.X, 0, moved.Z).Magnitude < 2.5
                    windowAt, windowPos = now, r.Position
                end
            end
            local stuck = pushing and (ground < 1.5 or creeping)
            local ledgeUp = ledge and climb
            if ghosting and now - ghostSince < 2.5 then stuck, ledgeUp = false, false end
            if stuck or ledgeUp then
                stuckSince = stuckSince or now
                local held = now - stuckSince
                if (held > 0.3 or ledgeUp) and not panicked then
                    panicked = true
                    if navFollowing() and targetLearn < 2 then
                        targetLearn += 1
                        navLearnAhead()
                        stuckSince, panicked = nil, false
                        windowAt, windowPos, creeping = nil, nil, false
                        task.wait()
                        continue
                    end
                    local goThrough = CFG.Ghost and dirT and targetGhosts < 2
                        and now >= ghostQuietUntil
                        and ((not CFG.Panic) or targetPanics >= 1)
                    if goThrough then
                        targetGhosts += 1
                        ghostOn(climb and "going up and through" or "going through")
                        stuckSince, panicked = nil, false
                        windowAt, windowPos, creeping = nil, nil, false
                        task.wait()
                        continue
                    elseif CFG.Panic and dirT and targetPanics < 4 then
                        targetPanics += 1
                        stats.panics += 1
                        local useClimb = ((targetPanics % 2 == 1) == climb)
                        local ok
                        if useClimb then
                            ok = climbBurst(target.root)
                        else
                            if lateralSide == nil then lateralSide = openSide(r, dirT) end
                            ok = lateralBurst(target.root, lateralSide)
                            if not ok then lateralSide = -lateralSide end
                        end
                        if ok then targetPanics = 0 end
                        stuckSince, panicked = nil, false
                        windowAt, windowPos, creeping = nil, nil, false
                        task.wait()
                        continue
                    end
                elseif panicked and held > 1.2 then
                    stuckSince, panicked = nil, false
                    windowAt, windowPos, creeping = nil, nil, false
                    targetPanics = 0
                    targetDetours += 1
                    stats.detours += 1
                    if targetDetours >= 3 then
                        unreachable = true
                    else
                        pathUntil = now + 8
                    end
                    task.wait()
                    continue
                end
            else
                stuckSince, panicked = nil, false
            end

            local noDash = climb or (stuckSince ~= nil) or (now - lastJumpAt < 1.2)
                or (navFollowing() and navPath ~= nil and #navPath > 2)
            local dashed = (not noDash)
                and tryDash(d, target.root.Position - r.Position) or false

            if closing and CFG.M1 and not dashed then
                stats.swings += 1
                pressM1()
            end
            progress()
            lastHitAt = os.clock()
            if closing then
                swingWait(hum, target.root, swingFrom)
            else
                task.wait(0.06)
            end
        end

        if hum.Health < lastHP - 0.5 then
            stats.damaging += 1
            lastHitAt = os.clock()
            progress()
        end
        lastHP = hum.Health
    end

    if target and target.hum and target.hum.Health > 0 then
        engagedModel = target.model
    else
        engagedModel = nil
    end

    if math.random() < 0.02 then
        local now = os.clock()
        for model, t in pairs(countedDead) do
            if now - t > 120 then countedDead[model] = nil end
        end
        for model in pairs(nameCache) do
            if not model.Parent then nameCache[model] = nil end
        end
    end

    if os.clock() - lastProgressAt > CFG.StuckSeconds then
        escalate(target)
    end
end

local mainGen, dogGen = 0, 0

local function mainLoop()
    mainGen += 1
    local gen = mainGen
    while P.running and gen == mainGen do
        local ok, err = pcall(step)
        if not ok then
            log("step error: " .. tostring(err))
            task.wait(0.6)
        end
        task.wait(0.05)
    end
end

local function watchdog()
    dogGen += 1
    local gen = dogGen
    local lastSeen, lastSwings = os.clock(), stats.swings
    while P.running and gen == dogGen do
        task.wait(5)
        if stats.swings ~= lastSwings then
            lastSwings = stats.swings
            lastSeen = os.clock()
        elseif os.clock() - lastSeen > 90 and state == "FIGHT" then
            escalation = 0
            setState("RESOLVE")
            lastSeen = os.clock()
        end
    end
end

local Window = Rayfield:CreateWindow({
   Name = "D0ggie Hub | Blox Fruits",
   LoadingTitle = "D0ggie Hub",
   LoadingSubtitle = "Blox Fruits Suite",
   ConfigurationSaving = {
      Enabled = true,
      FolderName = "D0ggieHub",
      FileName = "BloxFruits"
   }
})

local FarmTab = Window:CreateTab({ Name = "Farm" })
local TargetTab = Window:CreateTab({ Name = "Target" })
local WeaponTab = Window:CreateTab({ Name = "Weapon" })
local AttackTab = Window:CreateTab({ Name = "Attack" })
local SpeedTab = Window:CreateTab({ Name = "Speed" })
local QuestTab = Window:CreateTab({ Name = "Quest" })
local StatsTab = Window:CreateTab({ Name = "Stats" })

FarmTab:CreateSection("Master Control")
FarmTab:CreateToggle({
   Name = "Start Farm",
   CurrentValue = false,
   Flag = "BFP_Active",
   Callback = function(Value)
      if Value then
         P.start()
      else
         P.stop()
      end
   end,
})

FarmTab:CreateToggle({
   Name = "Quest Loop",
   CurrentValue = true,
   Flag = "BFP_QuestLoop",
   Callback = function(Value)
      CFG.QuestLoop = Value
      if Value then P.armQuest() end
   end,
})

TargetTab:CreateSection("Target Selection")
TargetTab:CreateInput({
   Name = "Custom Target Name",
   PlaceholderText = "e.g. Demonic Soul",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      if #Text > 0 then
         CFG.Target = Text
         activeName = nil
         P.lockedQuest = nil
         CFG.QuestName, CFG.QuestTier, CFG.QuestGiverName = nil, nil, nil
         setState("RESOLVE")
      end
   end,
})

TargetTab:CreateSlider({
   Name = "Max Walk Distance",
   Range = {200, 3000},
   Increment = 100,
   CurrentValue = 1200,
   Flag = "BFP_MaxWalk",
   Callback = function(Value)
      CFG.MaxWalk = Value
   end,
})

WeaponTab:CreateSection("Weapon Settings")
WeaponTab:CreateInput({
   Name = "Lock Weapon Name",
   PlaceholderText = "Leave empty for free hands",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      CFG.Weapon = (#Text > 0) and Text or nil
   end,
})

WeaponTab:CreateToggle({
   Name = "Auto Buso (Enhancement)",
   CurrentValue = true,
   Flag = "BFP_AutoBuso",
   Callback = function(Value)
      CFG.AutoBuso = Value
   end,
})

WeaponTab:CreateToggle({
   Name = "Auto Ken (Observation)",
   CurrentValue = true,
   Flag = "BFP_AutoKen",
   Callback = function(Value)
      CFG.AutoKen = Value
   end,
})

AttackTab:CreateSection("Combat & Movement")
AttackTab:CreateSlider({
   Name = "StandOff Distance",
   Range = {2, 40},
   Increment = 1,
   CurrentValue = 8,
   Flag = "BFP_StandOff",
   Callback = function(Value)
      CFG.StandOff = Value
   end,
})

AttackTab:CreateToggle({
   Name = "Terrain Map & Pathfinding",
   CurrentValue = true,
   Flag = "BFP_TerrainMap",
   Callback = function(Value)
      CFG.TerrainMap = Value
      if not Value then navHalt() end
   end,
})

AttackTab:CreateToggle({
   Name = "Walk Through Walls When Stuck",
   CurrentValue = true,
   Flag = "BFP_Ghost",
   Callback = function(Value)
      CFG.Ghost = Value
      if not Value then pcall(ghostRelease) end
   end,
})

AttackTab:CreateToggle({
   Name = "Gather Mobs",
   CurrentValue = true,
   Flag = "BFP_Gather",
   Callback = function(Value)
      CFG.Gather = Value
   end,
})

AttackTab:CreateSection("Skill Execution")
AttackTab:CreateToggle({
   Name = "Use M1",
   CurrentValue = true,
   Flag = "BFP_M1",
   Callback = function(Value) CFG.M1 = Value end,
})
AttackTab:CreateToggle({
   Name = "Use Skill Z",
   CurrentValue = false,
   Flag = "BFP_Z",
   Callback = function(Value) CFG.SkillZ = Value end,
})
AttackTab:CreateToggle({
   Name = "Use Skill X",
   CurrentValue = false,
   Flag = "BFP_X",
   Callback = function(Value) CFG.SkillX = Value end,
})
AttackTab:CreateToggle({
   Name = "Use Skill C",
   CurrentValue = false,
   Flag = "BFP_C",
   Callback = function(Value) CFG.SkillC = Value end,
})
AttackTab:CreateToggle({
   Name = "Use Skill V",
   CurrentValue = false,
   Flag = "BFP_V",
   Callback = function(Value) CFG.SkillV = Value end,
})

SpeedTab:CreateSection("Speed & Attacks")
SpeedTab:CreateSlider({
   Name = "Min Swing Gap",
   Range = {0.02, 1},
   Increment = 0.02,
   CurrentValue = 0.12,
   Flag = "BFP_SwingMin",
   Callback = function(Value) CFG.SwingMin = Value end,
})
SpeedTab:CreateSlider({
   Name = "Max Swing Gap",
   Range = {0.02, 1.5},
   Increment = 0.02,
   CurrentValue = 0.30,
   Flag = "BFP_SwingMax",
   Callback = function(Value) CFG.SwingMax = Value end,
})
SpeedTab:CreateToggle({
   Name = "Fast Attack",
   CurrentValue = false,
   Flag = "BFP_FastAttack",
   Callback = function(Value)
      CFG.FastAttack = Value
      if Value and not P.fastOK then installFastAttack() end
   end,
})
SpeedTab:CreateSlider({
   Name = "Attack Speed Rate",
   Range = {0.05, 2},
   Increment = 0.05,
   CurrentValue = 0.35,
   Flag = "BFP_AttackSpeed",
   Callback = function(Value) CFG.AttackSpeed = Value end,
})

QuestTab:CreateSection("Quest Settings")
QuestTab:CreateToggle({
   Name = "Return to Farm After Quest",
   CurrentValue = true,
   Flag = "BFP_Return",
   Callback = function(Value) CFG.QuestReturnToFarm = Value end,
})
QuestTab:CreateInput({
   Name = "Custom Quest ID",
   PlaceholderText = "e.g. HauntedQuest2",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text)
      CFG.QuestName = (#Text > 0) and Text or nil
      P.lockedQuest = nil
   end,
})

StatsTab:CreateSection("Live Telemetry")
local KillsLabel = StatsTab:CreateLabel("Kills: 0")
local StateLabel = StatsTab:CreateLabel("State: IDLE")

StatsTab:CreateButton({
   Name = "Reset Counters",
   Callback = function()
      for k in pairs(stats) do stats[k] = 0 end
      stats.startedAt = os.clock()
   end,
})

task.spawn(function()
   while true do
      pcall(function()
         KillsLabel:Set("Kills: " .. stats.kills)
         StateLabel:Set("State: " .. state .. " | Status: " .. statusLine)
      end)
      task.wait(0.5)
   end
end)

Rayfield:Notify({
   Title = "D0ggie Hub Loaded",
   Content = "Blox Fruits Gen 2 framework initialized successfully.",
   Duration = 5,
})

Rayfield:LoadConfiguration()

function P.start(name)
    if P.running then P.stop() end
    if type(name) == "string" and #name > 0 and name ~= CFG.Target then
        CFG.Target = name
        CFG.QuestName, CFG.QuestTier, CFG.QuestGiverName = nil, nil, nil
    end

    for k in pairs(stats) do stats[k] = 0 end
    stats.startedAt = os.clock()
    activeName  = nil
    farmSpot    = nil
    blacklist   = {}
    countedDead = {}
    escalation  = 0
    pathUntil   = 0
    lastProgressAt = os.clock()
    P.running   = true
    moveEnabled = true
    pcall(P.armQuest)
    setState("RESOLVE")

    keepWeapon()
    seenChar, seenCharAt = player.Character, os.clock() - 10
    busoTries = 0
    P.kenDone = false
    kenNextAt, kenVerifyAt, kenMisses, kenBlind = 0, nil, 0, false
    if CFG.AutoBuso and not hasBuso() then
        kenChar = nil
    else
        kenChar = player.Character
    end
    pcall(installFastAttack)

    blockAt = nil
    track(RunService.Heartbeat:Connect(function() pcall(ghostWatch) end))
    navHalt()
    local navErrors = 0
    track(RunService.Heartbeat:Connect(function()
        local ok, err = pcall(navTick)
        if not ok then
            navErrors += 1
            if navErrors >= 3 then
                CFG.TerrainMap = false
                navHalt()
            end
        end
    end))

    track(player.Idled:Connect(function()
        pcall(function()
            VirtualUser:CaptureController()
            VirtualUser:ClickButton2(Vector2.new())
        end)
    end))

    track(player.CharacterAdded:Connect(function()
        task.wait(2)
        if not (CFG.Weapon and #CFG.Weapon > 0) and lastHeld then
            for _ = 1, 12 do
                local char = player.Character
                local bp   = player:FindFirstChild("Backpack")
                local tool = bp and bp:FindFirstChild(lastHeld)
                local hum  = char and char:FindFirstChildOfClass("Humanoid")
                if tool and tool:IsA("Tool") and hum then
                    pcall(function() hum:EquipTool(tool) end)
                    break
                end
                task.wait(0.5)
            end
        end
        keepWeapon()
        pcall(installFastAttack)
        progress()
    end))

    task.spawn(mainLoop)
    task.spawn(watchdog)
end

function P.stop()
    P.running = false
    epoch += 1
    moveEnabled = false
    task.delay(0.3, function() moveEnabled = true end)
    pcall(releaseCamera)
    pcall(cancelWalk)
    if fastConn then pcall(function() fastConn:Disconnect() end) fastConn = nil end
    for _, c in ipairs(conns) do pcall(function() c:Disconnect() end) end
    table.clear(conns)
    pcall(ghostRelease)
    navHalt()
    setState("IDLE")
    say("stopped")
end

function P.stats() return stats end
function P.state() return state, statusLine, escalation end

task.spawn(function()
    while _G.BFP == P do
        pcall(keepWater)
        task.wait(0.25)
    end
end)

local deepConn
deepConn = RunService.Heartbeat:Connect(function()
    if _G.BFP ~= P then
        deepConn:Disconnect()
        parkFloor()
        return
    end
    pcall(deepTick)
end)
