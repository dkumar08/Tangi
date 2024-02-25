import UIKit

@main
class AppDelegate: UIResponder, UIApplicationDelegate {



    func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
        // Override point for customization after application launch.
        return true
    }

    // MARK: UISceneSession Lifecycle

    func application(_ application: UIApplication, configurationForConnecting connectingSceneSession: UISceneSession, options: UIScene.ConnectionOptions) -> UISceneConfiguration {
        // Called when a new scene session is being created.
        // Use this method to select a configuration to create the new scene with.
        return UISceneConfiguration(name: "Default Configuration", sessionRole: connectingSceneSession.role)
    }

    func application(_ application: UIApplication, didDiscardSceneSessions sceneSessions: Set<UISceneSession>) {
        // Called when the user discards a scene session.
        // If any sessions were discarded while the application was not running, this will be called shortly after application:didFinishLaunchingWithOptions.
        // Use this method to release any resources that were specific to the discarded scenes, as they will not return.
    }


}
import UIKit

class SceneDelegate: UIResponder, UIWindowSceneDelegate {

var window: UIWindow?


func scene(_ scene: UIScene, willConnectTo session: UISceneSession, options connectionOptions: UIScene.ConnectionOptions) {
        // Use this method to optionally configure and attach the UIWindow `window` to the provided UIWindowScene `scene`.
        // If using a storyboard, the `window` property will automatically be initialized and attached to the scene.
        // This delegate does not imply the connecting scene or session are new (see `application:configurationForConnectingSceneSession` instead).
        guard let _ = (scene as? UIWindowScene) else { return }
    }

func sceneDidDisconnect(_ scene: UIScene) {
        // Called as the scene is being released by the system.
        // This occurs shortly after the scene enters the background, or when its session is discarded.
        // Release any resources associated with this scene that can be re-created the next time the scene connects.
        // The scene may re-connect later, as its session was not necessarily discarded (see `application:didDiscardSceneSessions` instead).
    }

func sceneDidBecomeActive(_ scene: UIScene) {
        // Called when the scene has moved from an inactive state to an active state.
        // Use this method to restart any tasks that were paused (or not yet started) when the scene was inactive.
    }

func sceneWillResignActive(_ scene: UIScene) {
        // Called when the scene will move from an active state to an inactive state.
        // This may occur due to temporary interruptions (ex. an incoming phone call).
    }

func sceneWillEnterForeground(_ scene: UIScene) {
        // Called as the scene transitions from the background to the foreground.
        // Use this method to undo the changes made on entering the background.
    }
private var pageViewController: UIPageViewController?

private func createPageViewController() {
       let pageController = self.storyboard!.instantiateViewControllerWithIdentifier("QuizPageViewController") as! UIPageViewController
       pageController.dataSource = self

if pageInfo.count > 0 {
           let firstController = getItemController(0)!
           let startingViewControllers: NSArray = [firstController]
           pageController.setViewControllers(startingViewControllers as? [UIViewController], direction: UIPageViewControllerNavigationDirection.Forward, animated: false, completion: nil)
       }

pageViewController = pageController
addChildViewController(pageViewController!)
self.view.addSubview(pageViewController!.view)
pageViewController!.didMoveToParentViewController(self)
   }

   private func getItemController(itemIndex: Int) -> QuizPageItem? {
       if itemIndex < pageInfo.count {
           let CurrentQuizPageItem = self.storyboard!.instantiateViewControllerWithIdentifier("QuizPageItem") as! QuizPageItem
           CurrentQuizPageItem.itemIndex = itemIndex
           CurrentQuizPageItem.thisPageInfo = pageInfo[itemIndex]
           return CurrentQuizPageItem
       }

return nil
   }

   /*
       PageView Delegates
   */
   func pageViewController(pageViewController: UIPageViewController, viewControllerBeforeViewController viewController: UIViewController) -> UIViewController? {

let CurrentQuizPageItem = viewController as! QuizPageItem

if CurrentQuizPageItem.itemIndex > 0 {
           return getItemController(CurrentQuizPageItem.itemIndex - 1)
       }

return nil
   }

   func pageViewController(pageViewController: UIPageViewController, viewControllerAfterViewController viewController: UIViewController) -> UIViewController? {

let CurrentQuizPageItem = viewController as! QuizPageItem

if CurrentQuizPageItem.itemIndex + 1 < pageInfo.count {
           return getItemController(CurrentQuizPageItem.itemIndex + 1)
       }

return nil
   }
