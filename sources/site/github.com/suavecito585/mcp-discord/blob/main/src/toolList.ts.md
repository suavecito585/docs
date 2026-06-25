# Source: https://github.com/suavecito585/mcp-discord/blob/main/src/toolList.ts

[suavecito585](https://github.com/suavecito585) / **[mcp-discord](https://github.com/suavecito585/mcp-discord)** Public

forked from [barryyip0625/mcp-discord](https://github.com/barryyip0625/mcp-discord)

- [Notifications](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord) You must be signed in to change notification settings
- [Fork 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
- [Star 0](https://github.com/login?return_to=%2Fsuavecito585%2Fmcp-discord)
 

 

## FilesExpand file tree

 main

/

# toolList.ts

Copy path

Blame

More file actions

Blame

More file actions

## Latest commit

## History

[History](https://github.com/suavecito585/mcp-discord/commits/main/src/toolList.ts)

History

615 lines (615 loc) · 20.9 KB

 main

/

# toolList.ts

Copy path

Top

## File metadata and controls

- Code
 
- Blame
 

615 lines (615 loc) · 20.9 KB

[Raw](https://github.com/suavecito585/mcp-discord/raw/refs/heads/main/src/toolList.ts)

Copy raw file

Download raw file

Open symbols panel

Edit and raw actions

1

2

3

4

5

6

7

8

9

10

11

12

13

14

15

16

17

18

19

20

21

22

23

24

25

26

27

28

29

30

31

32

33

34

35

36

37

38

39

40

41

42

43

44

45

46

47

48

49

50

51

52

53

54

55

56

57

58

59

60

61

62

63

64

65

66

67

68

69

70

71

72

73

74

75

76

77

78

79

80

81

82

83

84

85

86

87

88

89

90

91

92

93

94

95

96

97

98

99

100

101

102

103

104

105

106

107

108

109

110

111

112

113

114

115

116

117

118

119

120

121

122

123

124

125

126

127

128

129

130

131

132

133

134

135

136

137

138

139

140

141

142

143

144

145

146

147

148

149

150

151

152

153

154

155

156

157

158

159

160

161

162

163

164

165

166

167

168

169

170

171

172

173

174

175

176

177

178

179

180

181

182

183

184

185

186

187

188

189

190

191

192

193

194

195

196

197

198

199

200

201

202

203

204

205

206

207

208

209

210

211

212

213

214

215

216

217

218

219

220

221

222

223

224

225

226

227

228

229

230

231

232

233

234

235

236

237

238

239

240

241

242

243

244

245

246

247

248

249

250

251

252

253

254

255

256

257

258

259

260

261

262

263

264

265

266

267

268

269

270

271

272

273

274

275

276

277

278

279

280

281

282

283

284

285

286

287

288

289

290

291

292

293

294

295

296

297

298

299

300

301

302

303

304

305

306

307

308

309

310

311

312

313

314

315

316

317

318

319

320

321

322

323

324

325

326

327

328

329

330

331

332

333

334

335

336

337

338

339

340

341

342

343

344

345

346

347

348

349

350

351

352

353

354

355

356

357

358

359

360

361

362

363

364

365

366

367

368

369

370

371

372

373

374

375

376

377

378

379

380

381

382

383

384

385

386

387

388

389

390

391

392

393

394

395

396

397

398

399

400

401

402

403

404

405

406

407

408

409

410

411

412

413

414

415

416

417

418

419

420

421

422

423

424

425

426

427

428

429

430

431

432

433

434

435

436

437

438

439

440

441

442

443

444

445

446

447

448

449

450

451

452

453

454

455

456

457

458

459

460

461

462

463

464

465

466

467

468

469

470

471

472

473

474

475

476

477

478

479

480

481

482

483

484

485

486

487

488

489

490

491

492

493

494

495

496

497

498

499

500

501

502

503

504

505

506

507

508

509

510

511

512

513

514

515

516

517

518

519

520

521

522

523

524

525

526

527

528

529

530

531

532

533

534

535

536

537

538

539

540

541

542

543

544

545

546

547

548

549

550

551

552

553

554

555

556

557

558

559

560

561

562

563

564

565

566

567

568

569

570

571

572

573

574

575

576

577

578

579

580

581

582

583

584

585

586

587

588

589

590

591

592

593

594

595

596

597

598

599

600

601

602

603

604

605

606

607

608

609

610

611

612

613

614

615

export const toolList \= \[

{

name: "discord\_create\_category",

description: "Creates a new category in a Discord server.",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

name: { type: "string" },

position: { type: "number" },

reason: { type: "string" }

},

required: \["guildId", "name"\]

}

},

{

name: "discord\_edit\_category",

description: "Edits an existing Discord category (name and position).",

inputSchema: {

type: "object",

properties: {

categoryId: { type: "string" },

name: { type: "string" },

position: { type: "number" },

reason: { type: "string" }

},

required: \["categoryId"\]

}

},

{

name: "discord\_delete\_category",

description: "Deletes a Discord category by ID.",

inputSchema: {

type: "object",

properties: {

categoryId: { type: "string" },

reason: { type: "string" }

},

required: \["categoryId"\]

}

},

{

name: "discord\_login",

description: "Logs in to Discord using the configured token",

inputSchema: {

type: "object",

properties: {

token: { type: "string" }

},

required: \[\]

}

},

{

name: "discord\_send",

description: "Sends a message to a specified Discord text channel. Optionally reply to another message by providing its message ID.",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

message: { type: "string" },

replyToMessageId: { type: "string" }

},

required: \["channelId", "message"\]

}

},

{

name: "discord\_get\_forum\_channels",

description: "Lists all forum channels in a specified Discord server (guild)",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" }

},

required: \["guildId"\]

}

},

{

name: "discord\_create\_forum\_post",

description: "Creates a new post in a Discord forum channel with optional tags",

inputSchema: {

type: "object",

properties: {

forumChannelId: { type: "string" },

title: { type: "string" },

content: { type: "string" },

tags: {

type: "array",

items: { type: "string" }

}

},

required: \["forumChannelId", "title", "content"\]

}

},

{

name: "discord\_get\_forum\_post",

description: "Retrieves details about a forum post including its messages",

inputSchema: {

type: "object",

properties: {

threadId: { type: "string" }

},

required: \["threadId"\]

}

},

{

name: "discord\_list\_forum\_threads",

description: "Lists all threads (posts) in a Discord forum channel, including both active and archived threads",

inputSchema: {

type: "object",

properties: {

forumChannelId: { type: "string", description: "The ID of the forum channel to list threads from" },

includeArchived: { type: "boolean", description: "Whether to include archived threads (default: true)", default: true },

limit: { type: "number", description: "Maximum number of archived threads to fetch (default: 100, max: 100)", minimum: 1, maximum: 100, default: 100 }

},

required: \["forumChannelId"\]

}

},

{

name: "discord\_reply\_to\_forum",

description: "Adds a reply to an existing forum post or thread",

inputSchema: {

type: "object",

properties: {

threadId: { type: "string" },

message: { type: "string" }

},

required: \["threadId", "message"\]

}

},

{

name: "discord\_create\_text\_channel",

description: "Creates a new text channel in a Discord server with an optional topic and parent category",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

channelName: { type: "string" },

topic: { type: "string" },

categoryId: { type: "string", description: "Parent category ID to place the channel under" }

},

required: \["guildId", "channelName"\]

}

},

{

name: "discord\_create\_forum\_channel",

description: "Creates a new forum channel in a Discord server, optionally under a category",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

name: { type: "string" },

topic: { type: "string", description: "The forum channel guidelines/description" },

categoryId: { type: "string", description: "The ID of the parent category to create the channel under" }

},

required: \["guildId", "name"\]

}

},

{

name: "discord\_edit\_channel",

description: "Edits a Discord channel's name, topic, parent category, or position",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string", description: "The ID of the channel to edit" },

name: { type: "string", description: "New name for the channel" },

topic: { type: "string", description: "New topic for the channel" },

parentId: { type: "string", description: "The ID of a category to move the channel under" },

position: { type: "number", description: "New position of the channel in the list" },

reason: { type: "string", description: "Reason for editing (shown in audit log)" }

},

required: \["channelId"\]

}

},

{

name: "discord\_delete\_channel",

description: "Deletes a Discord channel with an optional reason",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

reason: { type: "string" }

},

required: \["channelId"\]

}

},

{

name: "discord\_read\_messages",

description: "Retrieves messages from a Discord text channel. Supports date-based filtering via before/after/around params (accepts snowflake IDs or ISO 8601 dates).",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

limit: {

type: "number",

minimum: 1,

maximum: 100,

default: 50

},

before: { type: "string", description: "Snowflake ID or ISO 8601 date (e.g. '2025-03-01T00:00:00Z'). Get messages before this point." },

after: { type: "string", description: "Snowflake ID or ISO 8601 date (e.g. '2025-03-01T00:00:00Z'). Get messages after this point." },

around: { type: "string", description: "Snowflake ID or ISO 8601 date (e.g. '2025-03-01T00:00:00Z'). Get messages around this point." }

},

required: \["channelId"\]

}

},

{

name: "discord\_get\_server\_info",

description: "Retrieves detailed information about a Discord server including channels and member count",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" }

},

required: \["guildId"\]

}

},

{

name: "discord\_add\_reaction",

description: "Adds an emoji reaction to a specific Discord message",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

messageId: { type: "string" },

emoji: { type: "string" }

},

required: \["channelId", "messageId", "emoji"\]

}

},

{

name: "discord\_add\_multiple\_reactions",

description: "Adds multiple emoji reactions to a Discord message at once",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

messageId: { type: "string" },

emojis: {

type: "array",

items: { type: "string" }

}

},

required: \["channelId", "messageId", "emojis"\]

}

},

{

name: "discord\_remove\_reaction",

description: "Removes a specific emoji reaction from a Discord message",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

messageId: { type: "string" },

emoji: { type: "string" },

userId: { type: "string" }

},

required: \["channelId", "messageId", "emoji"\]

}

},

{

name: "discord\_get\_reaction\_users",

description: "Lists the users who reacted with a specific emoji to a Discord message. Uses REST fetch and does not require Gateway intents. Returns up to 100 users per call.",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

messageId: { type: "string" },

emoji: { type: "string", description: "Unicode emoji name (e.g. '🟢') or custom emoji name." },

limit: {

type: "number",

minimum: 1,

maximum: 100,

default: 100

}

},

required: \["channelId", "messageId", "emoji"\]

}

},

{

name: "discord\_delete\_forum\_post",

description: "Deletes a forum post or thread with an optional reason",

inputSchema: {

type: "object",

properties: {

threadId: { type: "string" },

reason: { type: "string" }

},

required: \["threadId"\]

}

},

{

name: "discord\_get\_forum\_tags",

description: "Gets all available tags for a Discord forum channel, including tag IDs, names, and emoji",

inputSchema: {

type: "object",

properties: {

forumChannelId: { type: "string", description: "The ID of the forum channel to get tags from" }

},

required: \["forumChannelId"\]

}

},

{

name: "discord\_set\_forum\_tags",

description: "Sets the available tags for a Discord forum channel. Replaces all existing tags.",

inputSchema: {

type: "object",

properties: {

forumChannelId: { type: "string", description: "The ID of the forum channel to set tags on" },

tags: {

type: "array",

description: "Array of tag objects to set on the forum channel",

items: {

type: "object",

properties: {

name: { type: "string", description: "Tag name" },

emoji: { type: "string", description: "Unicode emoji for the tag (e.g. '🔬')" },

moderated: { type: "boolean", description: "Whether only moderators can apply this tag (default: false)" }

},

required: \["name"\]

}

}

},

required: \["forumChannelId", "tags"\]

}

},

{

name: "discord\_update\_forum\_post",

description: "Updates a forum post's title, applied tags, archived status, or locked status. Tags can be specified by name or ID.",

inputSchema: {

type: "object",

properties: {

threadId: { type: "string", description: "The ID of the forum post/thread to update" },

name: { type: "string", description: "New title for the forum post" },

tags: { type: "array", items: { type: "string" }, description: "Tags to apply (by name or ID). Replaces all existing tags." },

archived: { type: "boolean", description: "Whether to archive or unarchive the post" },

locked: { type: "boolean", description: "Whether to lock or unlock the post" }

},

required: \["threadId"\]

}

},

{

name: "discord\_edit\_message",

description: "Edits a message previously sent by the bot. Only messages authored by the bot can be edited.",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string", description: "The ID of the channel containing the message" },

messageId: { type: "string", description: "The ID of the message to edit" },

content: { type: "string", description: "The new content for the message" }

},

required: \["channelId", "messageId", "content"\]

}

},

{

name: "discord\_delete\_message",

description: "Deletes a specific message from a Discord text channel",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

messageId: { type: "string" },

reason: { type: "string" }

},

required: \["channelId", "messageId"\]

}

},

{

name: "discord\_create\_webhook",

description: "Creates a new webhook for a Discord channel",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string" },

name: { type: "string" },

avatar: { type: "string" },

reason: { type: "string" }

},

required: \["channelId", "name"\]

}

},

{

name: "discord\_send\_webhook\_message",

description: "Sends a message to a Discord channel using a webhook",

inputSchema: {

type: "object",

properties: {

webhookId: { type: "string" },

webhookToken: { type: "string" },

content: { type: "string" },

username: { type: "string" },

avatarURL: { type: "string" },

threadId: { type: "string" }

},

required: \["webhookId", "webhookToken", "content"\]

}

},

{

name: "discord\_edit\_webhook",

description: "Edits an existing webhook for a Discord channel",

inputSchema: {

type: "object",

properties: {

webhookId: { type: "string" },

webhookToken: { type: "string" },

name: { type: "string" },

avatar: { type: "string" },

channelId: { type: "string" },

reason: { type: "string" }

},

required: \["webhookId"\]

}

},

{

name: "discord\_delete\_webhook",

description: "Deletes an existing webhook for a Discord channel",

inputSchema: {

type: "object",

properties: {

webhookId: { type: "string" },

webhookToken: { type: "string" },

reason: { type: "string" }

},

required: \["webhookId"\]

}

},

{

name: "discord\_list\_servers",

description: "Lists all Discord servers the bot is a member of",

inputSchema: {

type: "object",

properties: {},

required: \[\]

}

},

{

name: "discord\_search\_messages",

description: "Searches for messages in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string", description: "The ID of the Discord server (guild) to search within" },

content: { type: "string", description: "Search for messages containing specific text" },

authorId: { type: "string", description: "Filter messages by a specific user ID" },

mentions: { type: "string", description: "Filter messages that mention a specific user ID" },

has: { type: "string", description: "Filter messages that contain specific content types (e.g., link, embed, file, poll, image, video, sound, sticker, snapshot)", enum: \["link", "embed", "file", "poll", "image", "video", "sound", "sticker", "snapshot"\] },

maxId: { type: "string", description: "Filter messages with IDs less than this value (messages before this ID)" },

minId: { type: "string", description: "Filter messages with IDs greater than this value (messages after this ID)" },

channelId: { type: "string", description: "Filter messages within a specific channel ID" },

pinned: { type: "boolean", description: "Filter messages based on whether they are pinned" },

authorType: { type: "string", description: "Filter messages by author type (user, bot, webhook)", enum: \["user", "bot", "webhook"\] },

sortBy: { type: "string", description: "Sort results by 'timestamp' or 'relevance'", enum: \["timestamp", "relevance"\] },

sortOrder: { type: "string", description: "Sort order: 'desc' for descending or 'asc' for ascending", enum: \["desc", "asc"\] },

limit: { type: "number", description: "Maximum number of messages to return (default 25, max 100)" },

offset: { type: "number", description: "Number of messages to skip (for pagination)" }

},

required: \["guildId"\]

}

},

{

name: "discord\_list\_roles",

description: "Lists all roles in a Discord server with their properties",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" }

},

required: \["guildId"\]

}

},

{

name: "discord\_create\_role",

description: "Creates a new role in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

name: { type: "string" },

color: { type: "string", description: "Hex color string (e.g. '#FF0000') or color name" },

hoist: { type: "boolean", description: "Whether the role should be displayed separately in the sidebar" },

mentionable: { type: "boolean", description: "Whether the role can be mentioned by anyone" },

permissions: { type: "array", items: { type: "string" }, description: "Array of permission flag names (e.g. \['SendMessages', 'ViewChannel'\])" },

reason: { type: "string" }

},

required: \["guildId", "name"\]

}

},

{

name: "discord\_edit\_role",

description: "Edits an existing role in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

roleId: { type: "string" },

name: { type: "string" },

color: { type: "string", description: "Hex color string (e.g. '#FF0000') or color name" },

hoist: { type: "boolean" },

mentionable: { type: "boolean" },

permissions: { type: "array", items: { type: "string" }, description: "Array of permission flag names" },

position: { type: "number", description: "New position in the role hierarchy" },

reason: { type: "string" }

},

required: \["guildId", "roleId"\]

}

},

{

name: "discord\_delete\_role",

description: "Deletes a role from a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

roleId: { type: "string" },

reason: { type: "string" }

},

required: \["guildId", "roleId"\]

}

},

{

name: "discord\_assign\_role",

description: "Assigns a role to a member in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

userId: { type: "string" },

roleId: { type: "string" },

reason: { type: "string" }

},

required: \["guildId", "userId", "roleId"\]

}

},

{

name: "discord\_remove\_role",

description: "Removes a role from a member in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

userId: { type: "string" },

roleId: { type: "string" },

reason: { type: "string" }

},

required: \["guildId", "userId", "roleId"\]

}

},

{

name: "discord\_list\_members",

description: "Lists members in a Discord server with their roles",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

limit: { type: "number", description: "Maximum number of members to return (default 100, max 1000)", minimum: 1, maximum: 1000, default: 100 },

after: { type: "string", description: "User ID to paginate after" }

},

required: \["guildId"\]

}

},

{

name: "discord\_get\_member",

description: "Gets detailed information about a specific member in a Discord server",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

userId: { type: "string" }

},

required: \["guildId", "userId"\]

}

},

{

name: "discord\_create\_voice\_channel",

description: "Creates a new voice channel in a Discord server with an optional parent category",

inputSchema: {

type: "object",

properties: {

guildId: { type: "string" },

channelName: { type: "string" },

categoryId: { type: "string", description: "Parent category ID to place the channel under" },

userLimit: { type: "number", description: "Maximum number of users allowed (0 for unlimited)", minimum: 0, maximum: 99 },

reason: { type: "string" }

},

required: \["guildId", "channelName"\]

}

},

{

name: "discord\_set\_channel\_permissions",

description: "Sets permission overrides for a role or user on a channel or category",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string", description: "Channel or category ID" },

roleId: { type: "string", description: "Role or user ID to set permissions for" },

allow: { type: "array", items: { type: "string" }, description: "Permission flags to allow (e.g. \['ViewChannel', 'SendMessages'\])" },

deny: { type: "array", items: { type: "string" }, description: "Permission flags to deny (e.g. \['ViewChannel', 'SendMessages'\])" },

reason: { type: "string" }

},

required: \["channelId", "roleId"\]

}

},

{

name: "discord\_remove\_channel\_permissions",

description: "Removes all permission overrides for a role or user on a channel or category",

inputSchema: {

type: "object",

properties: {

channelId: { type: "string", description: "Channel or category ID" },

roleId: { type: "string", description: "Role or user ID to remove overrides for" },

reason: { type: "string" }

},

required: \["channelId", "roleId"\]

}

}

\];