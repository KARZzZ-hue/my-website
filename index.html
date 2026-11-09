// Vercel serverless function: GET /api/user?username=NAME

async function lookupUser(username) {
  // 1) username -> user id
  const idRes = await fetch("https://users.roblox.com/v1/usernames/users", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify({ usernames: [username], excludeBannedUsers: false }),
  });
  if (!idRes.ok) throw new Error("Roblox lookup failed (" + idRes.status + ")");
  const idData = await idRes.json();
  if (!idData.data || idData.data.length === 0) return null;
  const id = idData.data[0].id;

  // 2) user id -> profile details + avatar headshot
  const [profileRes, thumbRes] = await Promise.all([
    fetch("https://users.roblox.com/v1/users/" + id),
    fetch(
      "https://thumbnails.roblox.com/v1/users/avatar-headshot?userIds=" +
        id +
        "&size=420x420&format=Png&isCircular=false"
    ),
  ]);
  if (!profileRes.ok) throw new Error("Could not load profile (" + profileRes.status + ")");
  const profile = await profileRes.json();
  const thumb = thumbRes.ok ? await thumbRes.json() : null;

  return {
    id: profile.id,
    username: profile.name,
    displayName: profile.displayName,
    created: profile.created,
    isBanned: profile.isBanned,
    avatarUrl: thumb && thumb.data && thumb.data[0] ? thumb.data[0].imageUrl : null,
  };
}

module.exports = async (req, res) => {
  const username = String(req.query.username || "").trim();

  if (!username || username.length > 40) {
    return res.status(400).json({ error: "Enter a valid username." });
  }

  try {
    const user = await lookupUser(username);
    if (!user) {
      return res.status(404).json({ error: "No user found with that username." });
    }
    return res.status(200).json(user);
  } catch (err) {
    return res.status(502).json({ error: err.message });
  }
};
